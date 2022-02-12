# fennel

## set up

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

### [test] 実行

@`$HOME/.config/nvim`

```vim
:make | luafile lua/myplugin.lua
```
## マクロ

neovim インテグレータ

[hotpot](https://github.com/rktjmp/hotpot.nvim)

[aniseed](https://github.com/Olical/aniseed)

[zest](https://github.com/tsbohc/zest.nvim)
