# neovimの設定をlispで書く. 大筋

(meta:tag neovim lua fennel)

[fennel公式サイト](https://fennel-lang.org)

> Fennelはluaにコンパイルされるlispです．使いやすく. 読みやすいことを目的として開発されました．luaを直接書くのと比較してほとんどオーバヘッドがありません．


## プラグインを書く

1. プラグインファイルを置く

@`$HOME/.config/nvim/plugin/myplgin.vim`

```vim
lua require('myplugin')
```

2. Makefile

@`$HOME/.config/nvim/Makefile`

```Makefile
all: lua/myplugin.lua

lua/%.lua: fnl/%.fnl
	fennel --compile $< > $@
```

3. 実行

@`$HOME/.config/nvim`

```vim
:make | luafile lua/myplugin.lua

```

## プラグイン

#### syntax
- [fennel.vim](https://github.com/bakpakin/fennel.vim')

#### native fennel suppor

- [fennel-nvim](https://github.com/jaawerth/fennel-nvim')

## マクロ

neovim インテグレータ

- [hotpot](https://github.com/rktjmp/hotpot.nvim)

- [aniseed](https://github.com/Olical/aniseed)

- [zest](https://github.com/tsbohc/zest.nvim)

- [fennel-cljlib](https://github.com/andreyorst/fennel-cljlib/blob/master/init.fnl)

## config例

- [datwaft](https://github.com/datwaft/nvim.conf/blob/main/fnl/conf/settings.fnl) (金魚アイコン)

- [tsbohc](https://github.com/tsbohc/.garden/tree/master/etc/nvim_old/config/fnl/core) (zest使っている. 女の子の絵のアイコン)

- [alexaandru](https://github.com/alexaandru/nvim-config/tree/master/fnl) (白黒の顔写真のアイコン)

## fennel製プラグイン
- [ggandor](https://github.com/ggandor/lightspeed.nvim)

## 書き方

[reference](https://fennel-lang.org/reference)

#### neovim config 例

- [datwaft](https://github.com/datwaft/nvim.conf)

#### 書いてみる: selfとテーブル

lua

```lua
Keys = {}

function Keys:get_i() return self.n end

function Keys:set_i(key, description)
   self.i[key] = description
end

function Keys.new()
   local obj = {
      i = {},
   }
   return setmetatable(obj, {__index = Keys})
end
```

fennel

```lisp
(local map_register {
  :i {}
  :get_i (fn [self] self.i)
  :set_i (fn [self key command description]
          (tset self.i key [command description]))

(map_register:set_i "jj" "<esc>" "end insert mode")
(print (vim.inspect (map_register:get_i)))
```

生成されたlua

```lua
local map_register
local function _1_(self)
  return self.i
end
local function _2_(self, key, command, description)
  self.i[key] = {command, description}
  return nil
end
map_register = {i = {}, get_i = _1_, set_i = _2_}
map_register:set_i("jj", "<esc>", "end insert mode")
return print(vim.inspect(map_register:get_i()))
```

## マクロ?

macroをrequireする際はimport-macrosを使うことを推奨されている.

macrosに自分のマクロが登録されていない場合がある．

```fennel
(local fennel (require :fennel))

(fn my-searcher [module-name]
  (let [filename (.. "src/" module-name ".fnl")]
    (match (find-in-archive filename)
      code (values (partial fennel.eval code {:env :_COMPILER})
                   filename))))

(table.insert fennel.macro-searchers my-searcher)
```

でもfennelがないって言われた....

-> fennelをトランスパイルしたluaにはfennelのモジュールが無い!

### luaにfennelモジュールをインストール

#### 1. install luarockts

luarocktsはluaのパッケージマネージャ

```sh
$ brew install luarocks
```
#### 2. integrate fennel into lua code

```sh
$ sudo luarocks install fennel
```

ローカルにインストールする場合は

```sh
$ mkdir ~/.luarocks
$ luarocks --local install fennel
```

WARN 今回はグローバルにインストールする場合で話をすすめる.

```lua
require('fennel')
```

が動けばok! と思ったら...
-> nvimのluaとローカルのluaが違う😢

- luarocks パケージマネージャ
- heherocks バージョン管理

-> [nvim_rocks](https://github.com/theHamsta/nvim_rocks)nvimプラグイン


を使う.

-> packerで対応しているみたい

-> vimのluaからpathが通っていない.


```lua
local local_package_path = "./?.lua;/Users/cassin/.config/nvim/lua5.1/share/lua/5.1/?.lua;/Users/cassin/.config/nvim/lua5.1/share/lua/5.1/?/init.lua"
package.path = package.path..';'..local_package_path
```
https://github.com/wbthomason/packer.nvim/issues/283

で動いた


### マクロを読み込む

デフォルトのパス

```fennel
(local fennel (require :fennel))
(print fennel.macro-searchers)
```

なのでpathはこんな感じで与える．

@`init.fnl`

```fennel
;; ├── conf
;; │   ├── init.fnl
;; │   └── macros.fnl ← これを読みたい
(local fennel (require :fennel))
(fn my-searcher [module-name]
  (let [filename (.. "fnl/conf/" module-name ".fnl" )]
    (match (find-in-archive filename)
      code (values (partial fennel.eval code {:env :_COMPILER})
                   filename))))
(table.insert fennel.macro-searchers my-searcher)
```


```fennel
(import-macros {: setg} :fnl.conf.macros)
```

で読み込める


-> 読み込めていないことに気づく-> fennelの公式ページのmacro-searcherの部分がなくなってて草

-> てかluaからfennelのマクロ呼ぶのは普通しない

macro.fnlはトランスパイルしない

-> トランスパイルするには一個かませるのか

init.fnl -> (module-hoge.fnl -> macro.fnl)

#### 使えそうな関数

```fennel
(local (module-name file-name) ...)
(print module-name) ; conf
(print fennel.macro-path) ;

-> 結局init.fnlから呼び出すことになった
```
