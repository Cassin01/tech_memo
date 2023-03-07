[Luaでオブジェクト指向(再考)・・・継承について](http://invalid-log.blogspot.com/2015/05/lua.html)

[プロトタイプのオブジェクト指向¶](https://ie.u-ryukyu.ac.jp/~e085739/lua.hajime.4.html)

---
## バージョン管理

[luarocks/hererocks](https://github.com/luarocks/hererocks)








どのように[ms-jpg/lua-async-await](https://github.com/ms-jpq/lua-async-await)
が実装されているかについてのまとめになります．

## ms-jpq/lua-async-awaitの概要

### a.sync

a.syncはa.waitで設定されたco.yieldを一つずつ実行しながらコルーチンを展開する．

### a.wait

co.yieldを設定する．

### a.wrap

引数なしのコールバック関数を作る.


### コルーチン

一応, 簡単な例を示します．
```lua
-- コルーチンの本体
local function task(...)
    coroutine.yield("first") -- 処理を中断する
    return "second"
end

local task1 = coroutine.create(task) -- コルーチンの作成
local sucess, result = coroutine.resume(task1, ...) -- コルーチンの実行
print(result) -- `first`
local sucess, result = coroutine.resume(task1, ...) -- コルーチンの再開
print(result) -- `second`
```

### coroutine to async, await

ほぼ [ms-jpq/lua-async-await](https://github.com/ms-jpq/lua-async-await/blob/a1f0df179ccd9a8015c00673f0ef957158cb2937/README.md) の翻訳になります．

#### ミソ

async, awaitと coroutineの違いは,
RHSが準備できたらLHSに値を送ることです．

#### 同期的なコルーチン

準備運動のために
まずRHSがすでにできている同期的な例を用いて考えてきましょう.

これがコルーチンに値を渡す方法です．
```lua
co.resume(thread, x, y, z)
```

コアとなる考え方はcorutineをすべて展開されるまで繰り返すことです．

```lua
-- 再帰関数nxtを使ってコルーチンを展開する.
local pong = function (thread)
    local nxt = nil
    nxt = function (cont, ...)
        if not cont
        then return ...
        else return nxt(co.resume(thread, ...))
        end
    end
    return nxt(co.resume(thread))
end
```

`pong`にコルーチンを渡すと, 完全に展開されるまで再帰的にコルーチンが実行されます．

```lua
local thread = co.create(function ()
    local x = co.yield(1)
    print(x)
    local y, z = co.yield(2, 3)
    print(y)
end)
pong(thread)
```

実行すると以下のような結果が得られるでしょう．

```zsh
$ lua pong.lua
1
2       3

```

#### Thunk

<!-- 同期的な`pong`がどう動くかあなたが理解できたとしたら，私達はゴールにすごく近いところにいることになります． -->

`pong`の非同期的なバージョンを考えるために, 一つ簡単な
概念を紹介させてください．

`Thunk`はコールバック関数を引き呼び起こすことを目的とした関数です．


`Thunk`により関数の型は`(arg, callback) -> void` から `arg -> (callback -> void) -> void`

に変形されます．

```lua
-- Thankより，ファイルの読み込みが遅延される
local read_fs = function (file)
    local thunk = function (callback)
        -- callbackはfileが読み込まれたあと, 呼ばれる関数
        fs.read(file, callback)
    end

    return thunk
end

-- Thunkを使って変形するまえ
-- local read_fs = function (file)
--     fs.read(file, callback)
-- end
```

この`Thunk`による関数の型変形は自動化することができます．

```lua
local wrap = function (func)
    local factory = function(...)
        local params = {...}
        local thunk = function (step)
            table.insert(params, step)
            return func(unpack(params))
        end
        return thunk
    end
    return factory
end

local thunk = wrap(fs.read)
```
<!-- wrap()はfactory()を返す. -->
<!-- factory()はlocal.thunk()を返す． -->
<!-- auter.thunk() -->

では，なぜこれが必要なのでしょうか?

#### Async Await

答えは簡単です．私達のRHSにThunkを使うからです．

---

上の答えを言うとともに,

`step`関数というトリックを説明する必要があります．

`step`関数の唯一の仕事ははすべてのthunkにコールバック関数を置くことです．

重要なことは, それぞれのコールバックにおいて
coroutineの処理を一つ進めることです．

```lua
-- func: コルーチンの本体
-- callback: 最後に呼びたい関数
local pong = function (func, callback)
    assert(type(func) == "function", "type error :: expected func")
    local thread = co.create(func)
    local step = nil
    step = function (...)
        local stat, ret = co.resume(thread, ...)
        assert(stat, ret)
        if co.status(thread) == "dead" then
            -- これ以上resume()できなければ, callback関数を呼ぶ
            -- このときretはcallback関数に渡される引数`co.resume`の第2引数になる．
            (callback or function () end)(ret)
        else
            assert(type(ret) == "function", "type error :: expected func")
            ret(step)
        end
    end
    step()
end
```
pongは自身のコルーチンの展開処理が終わった後に`callback`関数を呼ぶことに気づくでしょう.

---

このことは以下のアクションで見ることができます．

```lua
local echo = function (...)
    local args = {...}
    local thunk = function (step)
        step(unpack(args))
    end
    reutrn thunk
end

local thread = co.create(function ()
    local x, y, z = co.yield(echo(1, 2, 3))
    print(x, y, z)
    local x, f, c = co.yield(echo(4, 2, 6))
    print(k, f, c)
    pong(thread)
end)
```

注意：ここでは説明のために同期エコーを使用しています。コールバックがいつ呼び出されるかは問題ではありません．この機構はタイミングに依存しません．

非同期は同期をより一般化したものと考えることができます.

最後のセクションで非同期バージョンを実行することができます.

#### Await All

thunkのさらなる利点は任意の計算をthunkに注入することができることです．

例えば，たくさんのthunkをつなげることなどです．

```lua
local join = function (thunks)
    local len = table.getn(thunks)
    local done = 0
    local acc = {}
    local thunk = function (step)
        if len == 0 then
            return step()
        end
        for i, tk in ipairs(thunks) do
            local callback = function (...)
                acc[i] = {...}
                done = done + 1
                if done == len then
                    step(unpack(acc))
                end
            end
            tk(callback)
        end
    end
end
```


## Luarocks version 指定
```
luarocks --lua-dir=/usr/local/opt/lua@5.1 install say
```
