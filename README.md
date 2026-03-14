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
