# neovimの設定をfennelで書く

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

### Reference

[reference](https://fennel-lang.org/reference)

### plugins

#### syntax

- [fennel.vim](https://github.com/bakpakin/fennel.vim')

#### native fennel support

- [fennel-nvim](https://github.com/jaawerth/fennel-nvim')

#### transpile and path setting

- [hotpot](https://github.com/rktjmp/hotpot.nvim)

- [aniseed](https://github.com/Olical/aniseed)

- [init.lua](https://git.sr.ht/~hauleth/dotfiles/tree/master/item/vim/.config/nvim/init.lua)

#### macro libralis

- [zest](https://github.com/tsbohc/zest.nvim)
- [fulib.nvim](https://github.com/6cdh/fulib.nvim)

### dotfiles

#### using aniseed
- [alexaandru](https://github.com/alexaandru/nvim-config/tree/master/fnl)
    - white and brack icon

- [camspiers/dotfiles](https://github.com/camspiers/dotfiles/blob/master/files/.config/nvim/fnl/options.fnl)
    - using aniseed, neat

- [nyoom.nvim](https://www.libhunt.com/topic/neovim-dotfiles)
    - full fennel

- [cat face icon](https://notabug.org/dm9pZCAq/dotfiles/src/master/.config/nvim)
    - all writen in fennel and all file will be compiled.

- [datwaft](https://github.com/datwaft/nvim.conf/blob/main/fnl/conf/settings.fnl)
    - producer of hotpot

- [tsbohc](https://github.com/tsbohc/.garden/tree/master/etc/nvim_old/config/fnl/core)
    - using zest

#### using hotpot

 - [girl icon](https://github.com/6cdh/dotfiles/tree/main/editor/nvim)
     - producer of fulib.nvim

## plugin for s-expressions

- [paredit](https://github.com/vim-scripts/paredit.vim)
    - ⭐ 168 (Im not using)

- [vim-sexp](https://github.com/guns/vim-sexp)
    - ⭐ 541

```
(a (b ...)) -> (a) (b ...)
(a) (b) -> (a b)
(a (b)) -> (b)
```

- [vim-sexp-mappings-for-regular-people](https://github.com/tpope/vim-sexp-mappings-for-regular-people)
    - ⭐ 368

- [parinfer](https://github.com/bhurlow/vim-parinfer)
    - ⭐ 161 (Im not using)
    - auto right-bracket complication and indentation

