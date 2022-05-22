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

