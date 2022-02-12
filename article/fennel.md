# neovimの設定をlispで書く

(meta:tag neovim lua fennel)

vim9? lua? python3? rust? deno?😵‍💫どれ使えばいいの?

という話題がホット(たぶん)

自分のconfigくらいlispで書いてもいいかも


[fennel公式サイト](https://fennel-lang.org)

## プラグインを書く

### 1. プラグインファイルを置く

@`$HOME/.config/nvim/plugin/myplgin.vim`

```vim
lua require('myplugin')
```

### 2. Makefile

@`$HOME/.config/nvim/Makefile`

```Makefile
all: lua/myplugin.lua

lua/%.lua: fnl/%.fnl
	fennel --compile $< > $@
```

### 実行

@`$HOME/.config/nvim`

```vim
:make | luafile lua/myplugin.lua

```

## プラグイン

### syntax
- [fennel.vim](https://github.com/bakpakin/fennel.vim')

### native fennel suppor

- [fennel-nvim](https://github.com/jaawerth/fennel-nvim')

## マクロ

neovim インテグレータ

- [hotpot](https://github.com/rktjmp/hotpot.nvim)

- [aniseed](https://github.com/Olical/aniseed)

- [zest](https://github.com/tsbohc/zest.nvim)

## config例

- [datwaft](https://github.com/datwaft/nvim.conf/blob/main/fnl/conf/settings.fnl)

## 書き方

[reference](https://fennel-lang.org/reference)

### neovim config 例

- [datwaft](https://github.com/datwaft/nvim.conf)

### 例: selfとテーブル

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
