# コマンドを非同期実行してみる

:vim:

## `luv`

`libuv`は`node.js`の非同期の部分で使われているらしいです.

`luv`は`luajit`の`libuv`バインディングです．

メソッドは`vim.loop`にあります．

詳しくは`:h vim.loop`


## コマンドを非同期実行する

```core/cmd.fnl
(fn u-cmd [name f ?opt]
       (let [opt (or ?opt {})]
         (tset opt :force true)
         (vim.api.nvim_create_user_command name f opt)))

;;; WARN: requires Cassin01/fetch-info
(u-cmd
  :MGInfo
  (λ [opts]
    (local {: async-cmd} (require :util.cmd))
    (async-cmd (.. "echom nvim_exec(\'GInfo" opts.args "\', v:true)")))
  {:nargs 1
   :complete (λ [ArgLead CmdLine CursorPos]
               [:F :C :J :W])})
```

```util/cmd.fnl
(local uv vim.loop)
(fn async-cmd [cmd]
  (local timer (uv.new_timer))
  (timer:start 1000 0
               (vim.schedule_wrap
                 (λ []
                   ; (print :Awake!)
                   (vim.cmd cmd)
                   (timer:close))))
```



## 供養

今までは[aktsk.jp](https://hackerslab.aktsk.jp/2020/12/receive-on-vim)の記事をコピーして使っていました．

### 使い方
- nvimを2つ起動する.
- はじめに立ち上げたものをサーバー用に使用する(colorschemeがkanagawaになる)


```server.vim
" Ref: https://hackerslab.aktsk.jp/2020/12/receive-on-vim

function s:handle(req) abort
  if a:req.method ==? 'POST'
    return {
          \   'status': 200,
          \   'status_text': 'OK',
          \   'body': execute(a:req.body, ""),
          \ }
  endif
  return {
        \   'status': 404,
        \   'status_text': 'Not Found',
        \   'body': json_encode(a:req),
        \ }
endfunction

function s:parse_request1(msg) abort
  let req = {}
  let matched = matchlist(a:msg, '^\v(.{-})\r\n\r\n(.*)')[1 : 2]
  let [header_block, body] = matched[1 : 2]
  let start_line = split(header_block, "\r\n")[0]
  let req.method = split(start_line, '\s\+')[0]
  let req.body = body
  return req
endfunction

function s:parse_body(msg) abort
  let start2read = v:false
  let ret = []
  for m in a:msg
    if start2read
      let ret = add(ret, m)
    endif
    if m =~ '^\r$'
      let start2read = v:true
    endif
  endfor
  return join(ret, "\n")
endfunction


function s:parse_request(msg) abort
  let req = {}
  let req.method = split(a:msg[0], '\s\+')[0]

  let req.body = s:parse_body(a:msg)
  return req
endfunction

function s:out_cb(job_id, data, event) abort
  try
    let req = s:parse_request(a:data)
    let res = s:handle(req)
  catch
    let res = {
          \   'status': 400,
          \   'status_text': 'Bad Request',
          \   'body': v:exception,
          \ }
  endtry

  let response = join([
        \   printf('HTTP/1.1 %d %s', res.status, res.status_text),
        \   'Content-Length: ' .. len(res.body),
        \   '',
        \   res.body,
        \ ], "\r\n")

  call luaeval('vim.api.nvim_chan_send(unpack(_A))', [a:job_id, response])
endfunction

function s:start(port) abort
  let job = jobstart(['ncat', '-lkp', a:port], {
        \   'on_stdout': function('s:out_cb'),
        \ })
endfunction

" {{{
function! s:port_scan_out_cb(job_id, data, event) abort
  if exists('g:cassin_cmd_server_portinfo')
    let g:cassin_cmd_server_portinfo = extend(g:cassin_cmd_server_portinfo, a:data)
  else
    let g:cassin_cmd_server_portinfo = a:data
  endif
endfunction

function! s:port_scan_exit_cb11111(job_id, data, event) abort
  if len(g:cassin_cmd_server_portinfo) == 1
    if !exists("g:cassin_cmd_server_job")
      let g:cassin_cmd_server_job = s:start('11111')
      let g:cassin_cmd_server_port = '11111'
      colorscheme kanagawa
    endif
  endif
endfunction
function! s:port_scan_exit_cb11112(job_id, data, event) abort
  if len(g:cassin_cmd_server_portinfo) == 1
    if !exists("g:cassin_cmd_server_job")
      let g:cassin_cmd_server_job = s:start('11111')
      let g:cassin_cmd_server_port = '11111'
    endif
  endif
endfunction

function s:port_scan(port) abort
  let job = jobstart(['lsof', '-P', '-i:' .. a:port], {
        \   'on_stdout': function('s:port_scan_out_cb'),
        \   'on_exit': function('s:port_scan_exit_cb'..a:port),
        \ })
  return job
endfunction
" }}}

call s:port_scan('11111')
" call s:port_scan('11112')

" curl -d 'echo "Hello, Vim server!"' 'localhost:11111'
" lsof -P -i:11111
```

```client.vim
(local vf vim.fn)
(fn show [str]
  (if (not= str nil)
    (print str)))
(fn out_cb [job_id data event]
  (show (. data 2)))
(fn start [cmd]
  (vf.jobstart ["curl" "-d" cmd "localhost:11111"]
               {:on_stdout out_cb }))

{: start}
```
