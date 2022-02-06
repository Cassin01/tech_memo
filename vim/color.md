# 色

## 特定の色をハイライトする

この方法ではコメント内部をハイライトできない

```vim
syntax match myT '\<NOTE\>'
highlight default link Todo myT
```

colorscheme 読み込み後に実行されるように、設定ファイルの colorscheme 読み込み部より前に記述する必要がある．

```vim
augruop colorschome_called
    autocmd!
    autocmd VimEnter, ColorScheme \*
augruop END
function! s:my_match()
    match TrailingSpaces ' \{-1,}$'
    match Tabs '\t'
    match ZenkakuSpace '\<　\>'
    match myT '"\<\(NOTE\|MARK\|OPTION\)\>'
endfunction
```

## 色を上書きする

```vim
highlight myT cterm=underline guifg=BLUE guibg=#cc0000
syntax match myT '\<NOTE\>'
highlight! link Todo myT
```

Todoの色で上書きされる．(Todoで設定されていない色(guifgなど)は上書きされない.)

