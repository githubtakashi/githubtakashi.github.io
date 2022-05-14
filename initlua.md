# init.luaファイルの設定メモ

nvimでinit.vimからinit.luaが推奨されているのでinit.luaで設定ファイルを  
作成するためのメモを書いていく。

[init.lua](https://neovim.io/doc/user/lua.html)のヘルプを参考までに参照する。

init.luaファイルを保存すべき場所は:checkhealthコマンドで確認できる。  
(init.vimと同じディレクトリでok)

22-04-08現在のinit.luaの内容|dell precision m6500 windows

```
local opt = vim.opt

opt.mouse = 'a'
opt.title = true
opt.ambiwidth = 'double'

opt.swapfile = false
opt.backup = false
opt.hidden = true
opt.clipboard:append({unnamedplus = true})

opt.syntax = 'on'
opt.incsearch = true
opt.hlsearch = true
opt.smartcase = true
opt.autoindent = true
opt.ruler = true
opt.laststatus = 2
opt.showcmd = true
opt.wildmenu = true
opt.virtualedit = 'onemore'
opt.filetype = "plugin", "indent","on"
opt.so = 5
opt.cursorline = true
opt.hidden = true

opt.number = true
opt.list = true
opt.smartindent = true
opt.visualbell = true

opt.showmatch = true

opt.expandtab = true
opt.tabstop = 4
opt.shiftwidth = 4

opt.listchars = 'tab:>-', 'trail:*', 'nbsp:+'
opt.ignorecase = true
opt.smartcase = true
opt.wrapscan = true

opt.whichwrap = 'b', 's', 'h', 'l', '<', '>', '[', ']'
opt.backspace = 'start', 'eol', 'indent'
opt.fileformats = 'dos', 'unix', 'mac'

opt.helplang = 'ja', 'en'

opt.updatetime = 300

opt.showtabline = 2
```
