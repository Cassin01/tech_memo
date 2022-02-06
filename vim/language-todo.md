

``matchadd()``を実行すると, matched list が増えてしまうので``s:matched(key)``をやっています．

## TOC

* [NOTE: TODO highlighting](#note:-todo-highlighting)
  * [[Annotation comment](https://qiita.com/taka-kawa/items/673716d77795c937d422)](#[annotation-comment](https://qiita.com/taka-kawa/items/673716d77795c937d422))
  * [[Atom language-todo](https://github.com/atom/language-todo)](#[atom-language-todo](https://github.com/atom/language-todo))
  * [[Atom language-todo-extention](https://github.com/BenjaminHoegh/language-todo-extended)](#[atom-language-todo-extention](https://github.com/benjaminhoegh/language-todo-extended))

## NOTE: TODO highlighting
DEFAULT: TODO FIXME HACK XXX WARNING

### [Annotation comment](https://qiita.com/taka-kawa/items/673716d77795c937d422)
- TODO: あとで追加、修正するべき機能がある。
- FIXME: 既知の不具合があるコード。修正が必要。
- HACK: あまりきれいじゃないコード。リファクタリングが必要。
- XXX: 危険！動くけどなぜうごくかわからない。
- REVIEW: 意図した通りに動くか、見直す必要がある。
- OPTIMIZE: 無駄が多く、ボトルネックになっている。
- CHANGED: コードをどのように変更したか。
- NOTE: なぜ、こうなったという情報を残す。
- WARNING: 注意が必要。

### [Atom language-todo](https://github.com/atom/language-todo)
- IDEA
- NB: 厄介なバグ `nasty bug` [what NB stands for][1]
- QUESTION: 疑問
- COMBAK: "I have something more urgent to do, let's mark this place so that I can COMBAK to it later" [what does the comment combak mean][2]
- TEMP: 一時的な
- DEBUG: [comments and debug code][3]
- OPTIMIZE: やれたらやる

[1]: https://forums.codeguru.com/showthread.php?177925-what-NB-stands-for "what NB stands for"
[2]: https://stackoverflow.com/questions/27411211/what-does-the-comment-combak-mean "what does the comment combak mean"
[3]: https://www.embeddedcomputing.com/technology/debug-and-test/probes-debuggers/comments-and-debug-code "comments and debug code"

### [Atom language-todo-extention](https://github.com/BenjaminHoegh/language-todo-extended)
- INFO
- REFACTOR
- DEPRECATED
- TASK
- UPDATE
- EXAMPLE
- ERROR
- WARN
- BROKEN

```vim
" Set color scheme {{{
    set background=dark
    if exists('g:my_color')
        exe("colo ". g:my_color)
    else
        echom 'Err: g:my_color is not exists. [at othermap.init.vim]'
    endif
" }}}

" 行末スペース、行末タブの表示 {{{
    "46 (緑), 240 (灰色), 50 (水色)
    highlight TrailingSpaces ctermbg=50 ctermfg=50 guibg=#FF0000 cterm=bold
    highlight Tabs ctermbg=black guibg=#eeeeec guibg=#FF0000
" }}}

" 全角スペースの表示 {{{
    highlight ZenkakuSpace cterm=underline ctermbg=BLUE guibg=#FF0000
" }}}

" Specific fords  {{{
    highlight TodoEX guifg=none guibg=#4e9a06
    highlight TodoEX2 guifg=none guibg=#c4a000
     highlight! link Todo TodoEX
     highlight! link Todo TodoEX2
" }}}
" match:
augroup call_match
    autocmd!
    autocmd ColorScheme * call s:my_match()
    autocmd BufRead,BufNew * call s:my_match()
augroup END
function! s:matched(key)
    for k in getmatches()
        if k['group'] == a:key
            return v:true
        endif
    endfor
    return v:false
endfunction
function! s:my_match()
    if s:matched('TodoEX')
        return
    endif

    call matchadd('TrailingSpaces', ' \+$')
    call matchadd('Tabs', '\t')
    call matchadd('ZenkakuSpace', '　')
    call matchadd('TodoEX', '\<\(NOTE\|MARK\|OPTION\|CHANGED\|IDEA\|REVIEW\|NB\|QUESTION\|COMBAK\|TEMP\|DEBUG\|OPTIMIZE\|REVIEW\)')
    call matchadd('TodoEX2', '\<\(INFO\|REFACTOR\|DEPRECATED\|TASK\|UPDATE\|EXAMPLE\|ERROR\|WARN\|BROKEN\)')
endfunction

" ## NOTE: TODO highlighting
" DEFAULT: TODO FIXME HACK XXX WARNING
"
" ### [annotation comment](https://qiita.com/taka-kawa/items/673716d77795c937d422)
" - TODO: あとで追加、修正するべき機能がある。
" - FIXME: 既知の不具合があるコード。修正が必要。
" - HACK: あまりきれいじゃないコード。リファクタリングが必要。
" - XXX: 危険！動くけどなぜうごくかわからない。
" - REVIEW: 意図した通りに動くか、見直す必要がある。
" - OPTIMIZE: 無駄が多く、ボトルネックになっている。
" - CHANGED: コードをどのように変更したか。
" - NOTE: なぜ、こうなったという情報を残す。
" - WARNING: 注意が必要。
"
" ### [atom language-todo](https://github.com/atom/language-todo)
" - IDEA
" - NB: 厄介なバグ `nasty bug` [1][]
" - QUESTION: 疑問
" - COMBAK: ”I have something more urgent to do, let's mark this place so that I can COMBAK to it later” [2][]
" - TEMP: 一時的な
" - DEBUG: [3][]
" - OPTIMIZE: やれたらやる
" ### ref
" - [1]: https://forums.codeguru.com/showthread.php?177925-what-NB-stands-for
" - [2]: https://stackoverflow.com/questions/27411211/what-does-the-comment-combak-mean
" - [3]: https://www.embeddedcomputing.com/technology/debug-and-test/probes-debuggers/comments-and-debug-code
"
" ### [atom language-todo-extention](https://github.com/BenjaminHoegh/language-todo-extended)
" - INFO
" - REFACTOR
" - DEPRECATED
" - TASK
" - UPDATE
" - EXAMPLE
" - ERROR
" - WARN
" - BROKEN
```
