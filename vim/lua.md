# lua

## 書き方

[Everything you need to know to configure neovim using lua](https://vonheikemen.github.io/devlog/tools/configuring-neovim-using-lua/)
## autocmd


[[Demo] Lua Augroups - Why And How To Use?](https://www.youtube.com/watch?v=F6GNPOXpfwUv)


# (x ...) not (... x)

[reddit](https://stackoverflow.com/questions/32439689/table-unpack-only-returns-the-first-element)

## vim.loop

[doc](https://github.com/luvit/luv/blob/master/docs.md)

[Using LibUV in Neovim](https://teukka.tech/vimloop.html)

### NOTE

In order for any vim functions to be called within a lua loop callback, they need to be wrapped in vim.schedule_wrap. Wrapping vim functions in vim.schedule_wrap is necessary since it schedules the callbacks to be invoked when it is safe, bridging the gap between the libuv event loop and the internal Neovim main loop.
