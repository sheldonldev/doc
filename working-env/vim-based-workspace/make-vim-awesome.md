# Make Vim Awesome


```bash
" --- Main Settings ---"

syntax on
set showcmd
set cmdheight=2
set ruler
set laststatus=2
set wildmenu
set hidden
set showmatch
set encoding=UTF-8
set termencoding=UTF-8

set confirm                     "raise an asking dialog instead of failling command when saving files"
set visualbell                  "use visual bell instead of error beeping"
set t_vb=""                     "set null to visualbell, now no warning anymore when hit the end of line"

set tabstop=4                   "4 chars long"
set softtabstop=4               "4 spaces long"
set shiftwidth=4                "4 spaces if press arrow key"
set expandtab                   "convert tabs to spaces"
set smartindent                 "try best job to indent for you"

set nu                          "nice line numbers"
set nowrap                      "no wrap if line too long"

set noswapfile                  "no need swap because we use undodir"
set nobackup                    "no need backup either"
set undodir=~/.vim/undodir      "for save undo files"
set undofile                    "an undo file per file"

set incsearch                   "get result while entering"
set hlsearch                    "highlight searches"
set smartcase                   "case sensitive searching"

set clipboard=unnamed           "in MacOS, or use 'unnamedplus' otherwise"

set colorcolumn=80
highlight ColorColumn ctermbg=0 guibg=lightgrey


" --- Auto Complete Braces and Quotes --- "

inoremap { {}<Esc>ha
inoremap [ []<Esc>ha
inoremap ( ()<Esc>ha
inoremap < <><ESC>ha

inoremap ' ''<Esc>ha
inoremap " ""<Esc>ha    ""ignore this comment, just to make the quote paired"
inoremap ` ``<Esc>ha

inoremap % %%<Esc>ha


" --- set <leader> key ---"
let mapleader = " "


" --- Jump between windows --- "
nnoremap <leader>h :wincmd h<CR>
nnoremap <leader>j :wincmd j<CR>
nnoremap <leader>k :wincmd k<CR>
nnoremap <leader>l :wincmd l<CR>


" --- quickly open explorer --- "
nnoremap <leader>pv :wincmd v<bar> :Ex <bar> :vertical resize 25<CR>


" --- quickly adjust window size --- "
nnoremap <silent> <leader>] :vertical resize +10<CR>
nnoremap <silent> <leader>[ :vertical resize -10<CR>
nnoremap <silent> <leader>= :resize +5<CR>
nnoremap <silent> <leader>- :resize -5<CR>
nnoremap <silent> <leader>va :vertical resize 100<CR>
nnoremap <silent> <leader>ha :resize 30<CR>


" --- netrw sidewindow --- "
let g:netrw_preview   = 0
let g:netrw_alto      = 0
let g:netrw_liststyle = 3
let g:netrw_browse_split = 2
let g:netrw_winsize = 25
let g:netrw_banner = 0


" --- Finding Files ---- "

" search down for subfolders"
" provides tab-completion for all file related tasks"
set path+=**

" display all matching files when we tab complete"
set wildmenu

" Now you can us :find with tab"
" and use :b with incomplete match by just entering <CR> "


" --- Trim white space --- "

fun! TrimWhiteSpace()
    let l:save = winsaveview()
    keeppatterns %s/\s\+$//e
    call winrestview(l:save)
endfun

autocmd BufWritePre * :call TrimWhiteSpace()
```

## Basic Commands

### Start

```bash
vim -o file1 file2 file3
# -o is horizon
# -O is vertical
```

### Windows

```bash
:new
:vne[w]
:vs[plit]

:h opening-window
```

```bash
:h window-moving
```

```bash
:h window-resize
```

### Search Files

```bash
:Rg           # regex
:find _file_
:b _file_
:ls           # buffer list
```

### netrw

- It's a built in plugin now

```bash
:h netrw
```

