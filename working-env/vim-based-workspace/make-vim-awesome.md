# Make Vim Awesome

## Awesome Commands

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

:h window-moving

:h window-resize
```

### Search Files

```bash
:Rg           # regex search
:find _file_  # find file in root
:ls           # buffer list
:b _file_     # find file in buffer
```

### netrw

- It's a built-in plugin now

```bash
:h netrw
```

## Awesome Settings

- The following documentation is my first version of `.vimrc`, continuous updating is on GitHub:

{% embed url="https://github.com/sheldonldev/nvim_config" caption="My Vim Config on GitHub" %}

```bash
syntax enable
set showcmd
set cmdheight=2
set pumheight=10        " Makes popup menu smaller "

set ruler               " Ruler in status line "
set laststatus=2        " Always display the status line "
set showtabline=2       " Always show tabs "
set showmatch
set noshowmode          " We don't need to see things like -- INSERT -- anymore "

set hidden              " Required to keep multiple buffers open multiple buffers "

set encoding=UTF-8      " the encoding displayed"
set termencoding=UTF-8
set fileencoding=UTF-8  " The encoding written to file "

set splitbelow          " Horizontal splits will automatically be below "
set splitright          " Vertical splits will automatically be to the right "

set nowritebackup       " This is recommended by coc "
set updatetime=300      " Fast completion "
set timeoutlen=500      " Default is 1000 "
set shortmess+=c
set iskeyword+=-        " treat dash separated words as a word text object"
set signcolumn=yes

set confirm             " raise an asking dialog instead of failling command when saving files "
set visualbell          " use visual bell instead of error beeping "
set t_vb=""             " set null to visualbell, now no warning anymore when hit the end of line "

set tabstop=2           " chars long "
set softtabstop=2       " spaces long "
set shiftwidth=2        " spaces if press > "
set expandtab           " convert tabs to spaces "
set smarttab            " Makes tabbing smarter will realize you have 2 vs 4 "
set autoindent
set smartindent         " try best job to indent for you "

set nu                  " nice line numbers "
set relativenumber      " relative line number "
set nowrap              " no wrap if line too long "

set noswapfile                  " no need swap because we use undodir "
set nobackup                    " no need backup either "
set undodir=~/.vim/undodir      " for save undo files "
set undofile                    " an undo file per file "

set incsearch                   " get result while entering "
set hlsearch                    " highlight searches "
set smartcase                   " case sensitive searching "

set clipboard=unnamed           " in MacOS, or use `unnamedplus` otherwise "

set t_Co=256                    " Support 256 colors "
set colorcolumn=80
highlight ColorColumn ctermbg=0 guibg=lightgrey

set conceallevel=0              " So that I can see `` in markdown files "

" --- blink bar ---"
set guicursor=n-v-c:block,i-ci-ve:ver25,r-cr:hor20,o:hor50
        \,a:blinkwait700-blinkoff400-blinkon250-Cursor/lCursor
        \,sm:block-blinkwait175-blinkoff150-blinkon175


" --- Finding Files ---- "

" search down for subfolders "
" provides tab-completion for all file related tasks "
set path+=**

" display all matching files when we tab complete "
set wildmenu

" Now you can us :find with tab "
" and use :b with incomplete match by just entering <CR> "


" --- Auto Complete Braces and Quotes --- "

inoremap { {}<Esc>ha
inoremap [ []<Esc>ha
inoremap ( ()<Esc>ha
inoremap < <><ESC>ha

inoremap ' ''<Esc>ha
inoremap " ""<Esc>ha
inoremap ` ``<Esc>ha

inoremap % %%<Esc>ha


" --- set <leader> key --- "
let mapleader = " "


" --- Jump between windows --- "
nnoremap <leader>l :wincmd l<CR>
nnoremap <leader>h :wincmd h<CR>
nnoremap <leader>k :wincmd k<CR>
nnoremap <leader>j :wincmd j<CR>


" --- quickly adjust window size --- "
nnoremap <silent> <leader>] :vertical resize +10<CR>
nnoremap <silent> <leader>[ :vertical resize -10<CR>
nnoremap <silent> <leader>= :resize +5<CR>
nnoremap <silent> <leader>- :resize -5<CR>
nnoremap <silent> <leader>ll :vertical resize 100<CR>
nnoremap <silent> <leader>hh :vertical resize 25<CR>
nnoremap <silent> <leader>kk :resize 35<CR>
nnoremap <silent> <leader>jj :resize 5<CR>


" --- Alternate way to save, quit --- "
nnoremap <C-s> :wa<CR>
nnoremap <C-Q> :q<CR>


" --- <TAB>: completion --- "
inoremap <expr><TAB> pumvisible() ? "\<C-n>" : "\<TAB>"


" --- netrw sidewindow --- "
let g:netrw_preview   = 0
let g:netrw_alto      = 0
let g:netrw_liststyle = 3
let g:netrw_browse_split = 2
let g:netrw_winsize = 25
"" let g:netrw_banner = 0


" --- quickly open netrw explorer --- "
nnoremap <leader>pv :wincmd v<bar> :Ex <bar> :vertical resize 25<CR>


" --- Trim white space --- "

fun! TrimWhiteSpace()
  let l:save = winsaveview()
  keeppatterns %s/\s\+$//e
  call winrestview(l:save)
endfun

autocmd BufWritePre * :call TrimWhiteSpace()

```
