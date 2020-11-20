# Nvim for Web Dev

## Install Node

* An important plugin of Neovim is `coc.nvim`, which depends on NodeJS.
* `npm` provides a lot of tools for web development, such as `browser-sync`.
* So let's install node as well as the global npm packages by following this link.

{% embed url="https://doc.sheldonl.dev/working-env/toolkits/nodejs-and-npm#installation" caption="NodeJS and npm packages Installation" %}


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

" append other nvim settings after "
```

* run command `:checkhealth` to show todo list


## Awesome Settings for Neovim

- Integrated Terminal

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

* I use `vim-plugin` as plugin manager

```bash
# repo: https://github.com/junegunn/vim-plug
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

* How to use `vim-plugin`:

```bash
" Append in ~/.config/nvim/init.vim "

" Call plugins "
call plug#begin('~/.vim/plugged')
Plug 'vender1/plug1'
Plug 'vender2/plug2'
Plug 'morevender/moreplug'
call plug#end()
```

* Run `:w`, `:PlugInstall`/`:PlugUpdate`/`PlugClear`


## Dependencies For the Plugins

The following dependencies is required:

* [nerd-font](https://github.com/ryanoasis/nerd-fonts#font-installation") for `vim-devicons`;
* [the_silver_searcher](https://github.com/ggreer/the_silver_searcher) for `fzf.vim`;

More details will be explained as we go.


## Neovim Plugins

### Visual Easier

```bash
" color scheme: https://github.com/morhetz/gruvbox "
Plug 'morhetz/gruvbox'

" relative line number: https://github.com/jeffkreeftmeijer/vim-numbertoggle "
Plug 'jeffkreeftmeijer/vim-numbertoggle'

" filetype icons, https://github.com/ryanoasis/vim-devicons "
" it requires Nerd Font, https://github.com/ryanoasis/nerd-fonts#font-installation "
" then, pleas set terminal preferences to choose this font for text "
Plug 'ryanoasis/vim-devicons'
" it will generate icon for plugins such as nerdtree and airline "

" nerdtree, https://github.com/preservim/nerdtree "
Plug 'preservim/nerdtree'

" airline also, https://github.com/vim-airline/vim-airline "
Plug 'vim-airline/vim-airline'
```

* NERDTree settings:

```bash
let g:NERDTreeShowHidden = 1
let g:NERDTreeMinimalUI = 1
let g:NERDTreeIgnore = []
let g:NERDTreeStatusline = ''

" Automaticaly close nvim if NERDTree is only thing left open "
autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) | q | endif

" Toggle "
nnoremap <silent> <leader>e :NERDTreeToggle<CR>
```

### Language Support

```bash
" Language Client and Extentions "
Plug 'neoclide/coc.nvim', {'branch': 'release'}
let g:coc_global_extensions = ['coc-emmet', 'coc-css', 'coc-html', 'coc-json', 'coc-prettier', 'coc-tsserver']

" TypeScript Highlighting "
Plug 'leafgarland/typescript-vim'
Plug 'peitalin/vim-jsx-typescript'
```

* coc settings:

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


" more: https://ianding.io/2019/07/29/configure-coc-nvim-for-c-c++-development/ "
```

* Run `:CocConfig`, add the following config:

```bash
{
  "coc.preferences.formatOnSaveFiletypes": ["javascript", "typescript", "typescriptreact", "json", "javascriptreact", "typescript.tsx"],
  "eslint.filetypes": ["javascript", "typescript", "typescriptreact", "javascriptreact", "typescript.tsx"],
  "coc.preferences.diagnostic.virtualText": true,
}
```


### Fuzzy Finder

* [fzf.vim](https://github.com/junegunn/fzf.vim)

```bash
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
Plug 'junegunn/fzf.vim'
```

* fzf settings:

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

## Save My Config on Github

- The above is my first version of `init.vim`, continuouse updating is on the github:

{% embed url="https://github.com/sheldonldev/nvim_config" caption="My Neovim Config on Github" %}

