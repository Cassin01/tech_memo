Number of star: 3/15

## vim

[amix](https://github.com/amix/vimrc)

26k

[spf13-vim](https://github.com/spf13/spf13-vim)

15.3k

[janus](https://github.com/carlhuda/janus)

7.9k

[k-vim](https://github.com/wklken/k-vim)

4.9k

[vimplus](https://github.com/chxuan/vimplus)

3.5k

[space-vim](https://github.com/liuchengxu/space-vim)

2.8k

[EverVim](https://github.com/LER0ever/EverVim)

## neovim

[LunerVim](https://github.com/LunarVim/LunarVim)

7.8k

[luan](https://github.com/luan/nvim)

[neovim-from-scratch](https://github.com/LunarVim/Neovim-from-scratch)

## plugin

```lua
use "moll/vim-bbye" --  Delete buffers (close files) without closing your windows or messing up your layout.
use "ahmedkhalf/project.nvim" -- プロジェクト単位でvimを操作
use "lewis6991/impatient.nvim" -- Speed up loading Lua modules in Neovim to improve startup time
use "antoinemadec/FixCursorHold.nvim" -- This is needed to fix lsp doc highlight


use "nvim-lua/popup.nvim"   -- An implementation of the Popup API from vim in Neovim
use "nvim-lua/plenary.nvim" -- Useful lua functions used ny lots of plugins
use "windwp/nvim-autopairs" -- Autopairs, integrates with both cmp and treesitter
use "numToStr/Comment.nvim" -- Easily comment stuff

-- LSP
use "neovim/nvim-lspconfig" -- enable LSP
use "williamboman/nvim-lsp-installer" -- simple to use language server installer
use "tamago324/nlsp-settings.nvim" -- language server settings defined in json for
use "jose-elias-alvarez/null-ls.nvim" -- for formatters and linters

-- tree-sitter
use "JoosepAlviste/nvim-ts-context-commentstring"

 -- Git
use "lewis6991/gitsigns.nvim" -- Show git status on left of a code.

-- cmp plugins
use "hrsh7th/nvim-cmp" -- The completion plugin
use "hrsh7th/cmp-buffer" -- buffer completions
use "hrsh7th/cmp-path" -- path completions
use "hrsh7th/cmp-cmdline" -- cmdline completions
use "saadparwaiz1/cmp_luasnip" -- snippet completions
use "hrsh7th/cmp-nvim-lsp"
```

```vim
Bundle 'tpope/vim-repeat'
Bundle 'rhysd/conflict-marker.vim'
" > Vim には、現在の編集セッションを保存するための ':mksession' コマンドがあります。 このプラグインは、Vim のセッションを専用の場所に保存し、全セッションの一覧表示、セッションを開く、最後のセッションを開く、セッションを閉じる、セッションを保存、最後のセッションを表示するコマンドを提供することにより、Vim のセッションを扱うことを支援するものです。 セッションのリストから、セッションを開く、セッションを削除する、セッションを編集する、追加セッションのスクリプトを編集することができます。 セッション名にはスペースを含めることができ、拡張子は.vimである必要はないことに注意してください。

" text writing
Bundle 'reedes/vim-litecorrect'

" auto correction for english writing
Bundle 'reedes/vim-textobj-sentence'
Bundle 'reedes/vim-textobj-quote' " streat quote -> curry quote
Bundle 'reedes/vim-wordy' " 誤用, 悪用, 過剰使用の履歴がある単語やフレーズを特定. リモートサーバにアクセスしない. 軽量.


" Web
Bundle 'mattn/webapi-vim'
```

**programming**

[echodoc.vim](https://github.com/Shougo/echodoc.vim)

[vim-wordchipper](https://github.com/preservim/vim-wordchipperv)

``<BS>`` or ``<C-h>``: Delete the character before the cursor
``<Del>``: Delete the character under the cursor
``<C-w>``: Delete the word before the cursor
``<C-u>``: Delete all characters before the cursor in the current line
In addition, with Ctrl-o you can execute a command, which will then return to Insert mode. For example <C-o>dw can delete the word after the cursor.

[undotree](https://github.com/mbbill/undotree)

```
" structlog makes logging in Lua less painful and more powerful by adding structure to your log entries.
```

### neovim plugin

logの構造化

[structlog](https://github.com/Tastyep/structlog.nvim)

#### snippet

[LuaSnip](https://github.com/L3MON4D3/LuaSnip/)

#### debug

[nvim-dap](https://github.com/mfussenegger/nvim-dap)

#### Terminal

[toggleterm](https://github.com/akinsho/toggleterm.nvim)

#### line theme

``nvim-lualine/lualine.nvim``

#### indent line

``lukas-reineke/indent-blankline.nvim``

#### dashboard

``goolord/alpha-nvim``


#### see also
