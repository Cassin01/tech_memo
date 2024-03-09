```yaml
title: plugin_development
date: 2024-03-09
categories: [programming]
tags: [lua, vim]
```

# プラグインをGitに上げずにローカルで試すためのminimal.lua

## 1. 下記のminimal.luaをプラグインがあるディレクトリと同じ階層に置く
```sh
❯ tree -L 1
.
├── lazy.nvim
├── minimal.lua
├── tokyonight.nvim
└── wf.nvim
```



<details>
<summary> minimal.lua </summary>


```lua
local root = vim.fn.fnamemodify("./.repro", ":p")
local plugins_path = vim.fn.fnamemodify("./", ":p")

-- set stdpaths to use .repro
for _, name in ipairs({ "config", "data", "state", "cache" }) do
  vim.env[("XDG_%s_HOME"):format(name:upper())] = root .. "/" .. name
end

local split = function(str)
  for i = 1, #str do
    local j = #str - i + 1
    if str:sub(j, j) == "/" then
      return str:sub(j+1, #str)
    end
  end
end

-- bootstrap lazy
local suck_my_git = function(plug_name)
-- "/plugins/lazy.nvim"
  local lazypath = plugins_path .. "/" .. split(plug_name)
  if not vim.loop.fs_stat(lazypath) then
    vim.fn.system({
        "git",
        "clone",
        "--filter=blob:none",
        "--single-branch",
        "https://github.com/" .. plug_name .. ".git",
        lazypath,
      })
  end
  vim.opt.runtimepath:prepend(lazypath)
end
suck_my_git("folke/lazy.nvim")
suck_my_git("Cassin01/wf.nvim")


vim.g.mapleader = " "

local plugins = {
  "folke/tokyonight.nvim",
  "Cassin01/wf.nvim"
}

require("lazy").setup(plugins, {
    -- root = root .. "/plugins",
    root = plugins_path
  })

local config = function()
  require("wf").setup()
end
config()

-- add anything else here
vim.opt.termguicolors = true
-- do not remove the colorscheme!
vim.cmd([[colorscheme tokyonight]])
```
</details>

## 2. `$ nvim -u minimal.lua`
