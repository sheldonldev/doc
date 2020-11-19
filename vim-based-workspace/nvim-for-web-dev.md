# Neovim for Web Development

- <https://medium.com/better-programming/setting-up-neovim-for-web-development-in-2020-d800de3efacd>
- <https://dev.to/fidelve/using-vim-as-your-main-editor-for-web-development-5a73>
## Install Neovim

```bash
brew install neovim
```

```bash
" edit ~/.config/nvim/init.vim to load ~/.vimrc "
set runtimepath^=~/.vim runtimepath+=~/.vim/after
let &packpath = &runtimepath
source ~/.vimrc

" disable python2 "
let g:loaded_python_provider = 0

" run command to show todo list "
:checkhealth
```

## Install Plugin Manager

- I use `vim-plugin` as plugin manager

```bash
# repo: https://github.com/junegunn/vim-plug
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

```bash
" Append in ~/.config/nvim/init.vim "

" Call plugins "

call plug#begin('~/.vim/plugged')

Plug 'vender1/plug1'
Plug 'vender2/plug2'
Plug 'morevender/moreplug'

call plug#end()

" You can append more settings and keymaps here following the caller "
```

## Node Packages for Neovim and Web Dev

- [Global Packages For Web Dev](/toolkits/nodejs-and-npm#global-packages-for-web-dev)

## Neovim Plugins

### vim-jsx-pretty

```bash
```

### vim-commentary

```bash
```

### ALE

```bash
```
