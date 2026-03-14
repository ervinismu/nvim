Minimal NVIM setup. With [lazy.nvim](https://lazy.folke.io/) as plugin manager.
### Pre
- [neovim](https://github.com/neovim/neovim)
- [ripgrep](https://github.com/BurntSushi/ripgrep) - FZF need it for searching text
### Structure
```
➜  tree nvim
~/.config/nvim
├── init.lua
├── lazy-lock.json
├── lua
│   ├── config
│   │   └── lazy.lua
│   └── plugins
│       ├── copilot.lua
│       ├── fzf.lua
│       ├── nvim-tree.lua
│       └── screenkey.lua

4 directories, 8 files
➜  
```

### Files
#### init.lua
```lua
require("config.lazy")

-- basic
vim.opt.number = true -- enable line numbering, usefull for showing current line number
vim.opt.relativenumber = true -- enable relative numbering, usefull for jump between line number
vim.opt.cursorline = true -- highlight cursor line horizontally
vim.opt.cursorcolumn = true -- highlight cursor line vertically
vim.g.loaded_netrw = 1 -- disabled netrw because use nvim-tree
vim.g.loaded_netrwPlugin = 1 -- disabled netrw because use nvim-tree

-- =================
-- >> VISUAL MODE <<
-- =================

-- disable arrow button - you can comment this(L10 - L13) if you want to use arrow keyboard
vim.keymap.set('v', '<Left>', ':echo "No Left, you can do it!"<CR>', { noremap = true })
vim.keymap.set('v', '<Right>', ':echo "No Left, you can do it!"<CR>', { noremap = true })
vim.keymap.set('v', '<Up>', ':echo "No Left, you can do it!"<CR>', { noremap = true })
vim.keymap.set('v', '<Down>', ':echo "No Left, you can do it!"<CR>', { noremap = true })


-- =================
-- >> NORMAL MODE <<
-- =================

-- disable arrow button - you can comment this(L10 - L13) if you want to use arrow keyboard
vim.keymap.set('n', '<Left>', ':echo "No Left, you can do it!"<CR>', { noremap = true })
vim.keymap.set('n', '<Right>', ':echo "No Left, you can do it!"<CR>', { noremap = true })
vim.keymap.set('n', '<Up>', ':echo "No Left, you can do it!"<CR>', { noremap = true })
vim.keymap.set('n', '<Down>', ':echo "No Left, you can do it!"<CR>', { noremap = true })

-- open screenkey using leader + s + k
vim.keymap.set("n", "<leader>sk", function() require("screenkey").toggle() end, { desc = "Toggle Screenkey" })

-- tabnew using leader + t + n
vim.keymap.set("n", "<leader>tn", ":tabnew<CR>", { desc = "Open New Tab" })

-- tabedit using leader + t + e
vim.keymap.set("n", "<leader>te", ":tabedit ", { desc = "Tab Edit" })

-- tabclose using leader + t + c
vim.keymap.set("n", "<leader>tc", ":tabclose<CR>", { desc = "Close Current Tab" })
```
#### lazy.lua
```lua
-- Bootstrap lazy.nvim
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not (vim.uv or vim.loop).fs_stat(lazypath) then
  local lazyrepo = "https://github.com/folke/lazy.nvim.git"
  local out = vim.fn.system({ "git", "clone", "--filter=blob:none", "--branch=stable", lazyrepo, lazypath })
  if vim.v.shell_error ~= 0 then
    vim.api.nvim_echo({
      { "Failed to clone lazy.nvim:\n", "ErrorMsg" },
      { out, "WarningMsg" },
      { "\nPress any key to exit..." },
    }, true, {})
    vim.fn.getchar()
    os.exit(1)
  end
end
vim.opt.rtp:prepend(lazypath)

-- Make sure to setup `mapleader` and `maplocalleader` before
-- loading lazy.nvim so that mappings are correct.
-- This is also a good place to setup other settings (vim.opt)
vim.g.mapleader = " "
vim.g.maplocalleader = "\\"

-- Setup lazy.nvim
require("lazy").setup({
  spec = {
    -- import your plugins
    { import = "plugins" },
  },
  -- Configure any other settings here. See the documentation for more details.
  -- colorscheme that will be used when installing plugins.
  install = { colorscheme = { "habamax" } },
  -- automatically check for plugin updates
  checker = { enabled = true },
})
```
#### fzf.lua
```lua
return {
  { 'junegunn/fzf', build = ':call fzf#install()' },
  {
    'junegunn/fzf.vim',
    keys = {
      { '<leader>ff', '<cmd>Files<cr>', desc = 'Find files' },
      { '<leader>fg', '<cmd>GFiles<cr>', desc = 'Find git giles' },
      { '<leader>ft', '<cmd>Rg<cr>', desc = 'Find text with RipGrep' },
    },
  }
}
```
#### nvim-tree.lua
```lua
return {
  "nvim-tree/nvim-tree.lua",
  version = "*",
  lazy = false,
  dependencies = {
    "nvim-tree/nvim-web-devicons",
  },
  cmd = { "NvimTreeToggle", "NvimTreeCollapse", "NvimTreeFindFile" },
  keys = {
    { "<leader>e", "<cmd>NvimTreeToggle<cr>", desc = "Explorer" },
    { "<leader>ef", "<cmd>NvimTreeFindFile<cr>", desc = "Explorer find file" },
    { "<leader>ec", "<cmd>NvimTreeCollapse<cr>", desc = "Collapse explorer" },
  },
  config = function()
    require("nvim-tree").setup {}
  end,
}
```
#### copilot.lua
```lua
return {
  "github/copilot.vim"
}
```
#### screenkey.lua
```lua
return {
    "NStefan002/screenkey.nvim",
    lazy = false,
    version = "*", -- or branch = "main", to use the latest commit
    config = function()
	require("screenkey").setup({
	    win_opts = {
		title = "", -- remove title bar
	        border = "rounded", -- rounded border
	    },
	    clear_after = 3, -- clear the keys after 3 seconds of inactivity
	})
    end,
}
```
