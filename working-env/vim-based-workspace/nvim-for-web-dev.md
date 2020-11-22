# Nvim for Web Dev

-   Complete config files are on GitHub:

{% embed url="https://github.com/sheldonldev/nvim_config" caption="My Neovim Config on GitHub" %}

## Install Node

-   `npm` provides a lot of tools for web development, such as `browser-sync`.
-   We use `coc.nvim` plugin as Language Server Protocol, which depends on NodeJS.

So let's install node as well as some global npm packages by following this link:

{% embed url="https://doc.sheldonl.dev/working-env/toolkits/nodejs-and-npm#installation" caption="NodeJS and npm packages Installation" %}

## Install Neovim

```bash
brew install neovim
```

-   Run command `:checkhealth` to show more todo list
-   Edit `~/.config/init.vim`:

```bash
" load ~/.vimrc and ~/.vim because I use vim before switched to nvim "
set runtimepath^=~/.vim runtimepath+=~/.vim/after
let &packpath = &runtimepath
source ~/.vimrc

" disable python2 because I just want to use python3"
let g:loaded_python_provider = 0
```

## Awesome Settings for Neovim

-   Basic settings are kept in `.vimrc` which can be found in
    [Make Vim Awsome](https://doc.sheldonl.dev/working-env/vim-based-workspace/make-vim-awesome)
-   Following settings can only be used in Neovim

### Integrated Terminal

```bash
" open new split panes to right and below "
set splitright
set splitbelow

" turn terminal to normal mode with escape "
tnoremap <Esc> <C-\><C-n>

" open terminal on ctrl+n "
function! OpenTerminal()
    split term://zsh          " I use zsh "
    resize 5
endfunction
nnoremap <C-n> :call OpenTerminal()<CR>
```

## Install Plugin Manager

-   I use `vim-plugin` as plugin manager

```bash
# repo: https://github.com/junegunn/vim-plug
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

-   Append plugins like following in `~/.config/nvim/init.vim`

```bash
call plug#begin('~/.vim/plugged')
Plug 'venderName/plugName'
Plug 'anotherVender/anotherPlug'
call plug#end()
```

-   Run `:w`, `:PlugInstall`/`:PlugUpdate`/`PlugClear`

## Plugin Installation and Settings

### Visual Easier

#### gruvbox

-   I prefer `gruvbox` as my theme.

```bash
" repo: https://github.com/morhetz/gruvbox "
Plug 'morhetz/gruvbox'

" settings "
colorscheme gruvbox
set background=dark
```

#### vim-numbertoggle

-   I prefer `vim-numbertoggle` to show relative line number which can make me move quicker.

```bash
" repo: https://github.com/jeffkreeftmeijer/vim-numbertoggle "
Plug 'jeffkreeftmeijer/vim-numbertoggle'

" settings "
set number relativenumber
```

#### vim-devicons, nerdtree, and airline

-   I prefer `vim-devicons` to show icons for different filetypes.
    -   It requires you install [Nerd Font](https://github.com/ryanoasis/nerd-fonts#font-installation)
    -   Then please set your terminal text font to Nerd Font.
    -   Now, `vim-devicons` will generate icons for other plugins such as `nerdtree` and `airline`.

```bash
" repo: https://github.com/ryanoasis/vim-devicons "
Plug 'ryanoasis/vim-devicons'
```

-   I use `nerdtree` as my explorer, and `airline` to show status bar.

````bash
" nerdtree, https://github.com/preservim/nerdtree "
Plug 'preservim/nerdtree'

" airline also, https://github.com/vim-airline/vim-airline "
Plug 'vim-airline/vim-airline'


" NERDTree settings "

```bash
let g:NERDTreeShowHidden = 1
let g:NERDTreeMinimalUI = 1
let g:NERDTreeIgnore = []
let g:NERDTreeStatusline = ''

" Automaticaly close nvim if NERDTree is only thing left open "
autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) | q | endif

" Toggle "
nnoremap <silent> <leader>e :NERDTreeToggle<CR>
````

### Language Support

#### coc.nvim

```bash
" Language Client and Extensions "
Plug 'neoclide/coc.nvim', {'branch': 'release'}
```

-   `coc` settings:

```bash
" Use tab for trigger completion with characters ahead and navigate. "
" Use command ':verbose imap <tab>' to make sure tab is not mapped by other plugin. "
inoremap <silent><expr> <TAB>
    \ pumvisible() ? "\<C-n>" :
    \ <SID>check_back_space() ? "\<TAB>" :
    \ coc#refresh()
inoremap <expr><S-TAB> pumvisible() ? "\<C-p>" : "\<C-h>"

function! s:check_back_space() abort
    let col = col('.') - 1
    return !col || getline('.')[col - 1] =~# '\s'
endfunction

" Use <cr> to confirm completion, `<C-g>u` means break undo chain at current position. "
" Coc only does snippet and additional edit on confirm. "
inoremap <expr> <cr> pumvisible() ? "\<C-y>" : "\<C-g>u\<CR>"

" Remap keys for gotos "
nmap <silent> gd <Plug>(coc-definition)
nmap <silent> gy <Plug>(coc-type-definition)
nmap <silent> gi <Plug>(coc-implementation)
nmap <silent> gr <Plug>(coc-references)

" Use K to show documentation in preview window "
nnoremap <silent> K :call <SID>show_documentation()<CR>

function! s:show_documentation()
    if (index(['vim','help'], &filetype) >= 0)
        execute 'h '.expand('<cword>')
    else
        call CocAction('doHover')
    endif
endfunction

" Highlight symbol under cursor on CursorHold "
autocmd CursorHold * silent call CocActionAsync('highlight')


" more: https://github.com/neoclide/coc.nvim"
```

-   Run `:CocConfig`, add the following config:

```bash
{
    "coc.preferences.formatOnSaveFiletypes":
        [
            "javascript",
            "typescript",
            "typescriptreact",
            "json",
            "javascriptreact",
            "typescript.tsx",
            "css",
            "markdown"
        ],
    "eslint.filetypes":
        [
            "javascript",
            "typescript",
            "typescriptreact",
            "javascriptreact",
            "typescript.tsx"
        ]
}
```

-   Install more coc extensions as you need and learn the usage: [Neoclide Repositories](https://github.com/neoclide/)

```bash
let g:coc_global_extensions = [
            \ 'coc-emmet',
            \ 'coc-css',
            \ 'coc-html',
            \ 'coc-json',
            \ 'coc-prettier',
            \ 'coc-tsserver',
            \ 'coc-vetur',
            \ 'coc-python',
            \ 'coc-yaml',
            \ 'coc-pairs',
            \ 'coc-eslint',
            \ 'coc-stylelint'
            \ ]
```

### Fuzzy Finder

-   [fzf.vim](https://github.com/junegunn/fzf.vim)

```bash
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
Plug 'junegunn/fzf.vim'
```

-   `fzf` settings:

```bash
nnoremap <C-p> :FZF<CR>
let g:fzf_action = {
  \ 'ctrl-t': 'tab split',
  \ 'ctrl-s': 'split',
  \ 'ctrl-v': 'vsplit'
  \}

" Tell fzf to use silversearcher-ag: "
" Install the_silver_searcher: https://github.com/ggreer/the_silver_searcher "
let $FZF_DEFAULT_COMMAND = 'ag -g ""'
```
