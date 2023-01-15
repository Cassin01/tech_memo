# vim

## Alternative marker for foldmethod.

Referenced from leap.nvim

```fennel
; vim: foldmethod=marker foldmarker=///,//>
```

## コマンドヒストリーを得る. Gets command history.

`histget('cmd', -1)`

## Use Normal-mode keymap at Insert-mode.

Use `(vim.api.nvim_set_keymap :i :<c-p> "<cmd>normal! j <cr>" ...)` but `i_CTRL-Q`.

## CapsLock
[Insert-mode_only_Caps_Lock](https://vim.fandom.com/wiki/Insert-mode_only_Caps_Lock)


## Get Info from outside of vim

[Vimで外部から情報を受け取る](https://hackerslab.aktsk.jp/2020/12/receive-on-vim)

On neovim, you can use `vim.loop` (`luv`) instead.

## Pass parameters to lua function from VimL

```vim
call luaeval("print(_A)", [1, 2, 3])
call luaeval('_A[1] + _A[2]', [1, 1])
echo luaeval('string.format("Lua is %s", _A)', 'awesome')
```

## Highhlight syntax inside Markdown

[Hightlight syntax inside Markdown](https://vimtricks.com/p/highlight-syntax-inside-markdown/)

```vim
let g:markdown_fenced_languages = ['cofee', 'css', 'json=javascript', 'erb=eruby']
```

## Operator-Pending Mappings

[Learn Vimscript the Hard Way](https://learnvimscriptthehardway.stevelosh.com/chapters/15.html)

## Adding hoooks to your neovim lua plugin using user events (usercmd).

[itmcho](https://itmecho.com/blog/neovim-lua-hooks-with-user-events)

## `:hi Ni(空白文字)(tab)`

ジョークコマンド


## Get window info
```txt
getwininfo([{winid}])					*getwininfo()*
		Returns information about windows as a |List| with Dictionaries.

		If {winid} is given Information about the window with that ID
		is returned, as a |List| with one item.  If the window does not
		exist the result is an empty list.

		Without {winid} information about all the windows in all the
		tab pages is returned.

		Each List item is a |Dictionary| with the following entries:
			botline		last complete displayed buffer line
			bufnr		number of buffer in the window
			height		window height (excluding winbar)
			loclist		1 if showing a location list
			quickfix	1 if quickfix or location list window
			terminal	1 if a terminal window
			tabnr		tab page number
			topline		first displayed buffer line
			variables	a reference to the dictionary with
					window-local variables
			width		window width
			winbar		1 if the window has a toolbar, 0
					otherwise
			wincol		leftmost screen column of the window;
					"col" from |win_screenpos()|
			textoff		number of columns occupied by any
					'foldcolumn', 'signcolumn' and line
					number in front of the text
			winid		|window-ID|
			winnr		window number
			winrow		topmost screen line of the window;
					"row" from |win_screenpos()|

		Can also be used as a |method|: >
			GetWinnr()->getwininfo()
```

## シェルからvimの出力を得る

```sh
$ vim -v -e -s -c "verbose smile" -c qa!
 # :smile:が出力される
```

# neovimのテスト

- [Releases, docs & tests for plugins](https://www.reddit.com/r/neovim/comments/103d9on/releases_docs_tests_for_plugins/)
- [boiler plate](https://github.com/shortcuts/neovim-plugin-boilerplate)



## vimのカーソルの設定

- [vimからの制御シーケンスの使用例](https://ttssh2.osdn.jp/manual/4/ja/usage/tips/vim.html)
- [Change your vim cursor from a black to line in normal and insert mode](https://youtu.be/FcQjTXLrVUU)

Use a line cursor within insert mode and a block cursor everywhere else.

Reference chart of values:
- Ps = 0 -> blinking block.
- Ps = 1 -> blinking block (default).
- Ps = 2 -> steady block.
- Ps = 3 -> blinking underline.
- Ps = 4 -> steady underline.
- Ps = 5 -> blinking bar (xterm)
- Ps = 6 -> steady bar (xterm)
