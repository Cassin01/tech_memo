```yaml
title: zsh
date: 2023-01-16
categories: [programming]
tags: [zsh]
```

#  zsh に割り当てれているキーバインドを調べる

```sh
$ bindkey | grep '"\^."'
"^@" set-mark-command
"^A" beginning-of-line
"^B" backward-char
"^D" delete-char-or-list
"^E" end-of-line
"^F" forward-char
"^G" send-break
"^H" backward-delete-char
"^I" fzf-completion
"^J" accept-line
"^K" kill-line
"^L" clear-screen
"^M" accept-line
"^N" down-line-or-history
"^O" accept-line-and-down-history
"^P" up-line-or-history
"^Q" push-line
"^R" fzf-history-widget
"^S" history-incremental-search-forward
"^T" fzf-file-widget
"^U" kill-whole-line
"^V" quoted-insert
"^W" backward-kill-word
"^Y" yank
"^]" ghq_src
"^_" undo
"^?" backward-delete-char
```

# .zshrcを読み込まずにzshを起動

```
$ zsh --no-rcs
```
