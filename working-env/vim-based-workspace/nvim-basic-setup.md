# Nvim Basic Setup

## Install Node

* `npm` provides a lot of tools for web development, such as `live-server`.
* We use `coc.nvim` plugin as Language Server, which depends on NodeJS.

> You can install node and some global npm packages by following this instruction:

{% embed url="https://doc.sheldonl.dev/working-env/toolkits/npm-and-yarn" caption="npm and yarn" %}

## Install Neovim

* Install [Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim) \(HEAD Version is recommended\)
* Run command `:checkhealth` to show more todo list.

## Awesome Settings for Neovim

* You can use Neovim like Vim by loading `.vimrc` in `~/.config/nvim/init.vim`.

  > Read [basic keymaps](https://doc.sheldonl.dev/working-env/vim-based-workspace/basic-keymaps) to learn basic vim motion; Read [make vim awesome](https://doc.sheldonl.dev/working-env/vim-based-workspace/make-vim-awesome) to set up your `.vimrc`. Check out [quickref](https://neovim.io/doc/user/quickref.html#quickref) to get complete info.

```bash
" load ~/.vimrc and ~/.vim because I use vim before switched to nvim "
set runtimepath^=~/.vim runtimepath+=~/.vim/after
let &packpath = &runtimepath
source ~/.vimrc
```

## Simple Plugins for Startup

### Plugin Manager

* Install plugin manager: [vim-plug](https://github.com/junegunn/vim-plug).

> Add following script to `init.vim` and run `:w`and `:source %` will help you install it automatically.

```bash
" auto-install vim-plug "
if empty(glob('~/.vim/autoload/plug.vim'))
  silent !curl -fLo ~/.nvim/autoload/plug.vim --create-dirs
    \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
endif
```

### Install Some Simple Plugins

* Now you can append plugins like the following in `init.vim`. the plugins' names are the names of their git repositories:

  > Remember, only single quote is recognizable in vim script, double quote is for commentary.

```bash
call plug#begin('~/.vim/plugged')
Plug 'sheldonldev/gruvbox'
Plug 'sheerun/vim-polyglot'
Plug 'psliwka/vim-smoothie'
Plug 'Yggdroot/indentLine'
call plug#end()
```

* Run `:w`and `:source %`, then run `:PlugInstall`/`:PlugUpdate`/`:PlugClean`/`:PlugStatus`/`:PlugDiff`.
* Now you should read the documentation in the repositories to set up your plugins.
* For simple plugin settings, it is OK to add configuations in `init.vim`. The followings are some examples.

#### gruvbox

* `gruvbox` is one of the most welcome editor theme.
* [My gruvbox](https://github.com/sheldonldev/gruvbox) is forked from [morhetz/gruvbox](https://github.com/morhetz/gruvbox):
  * just slightly increase some contrast;
  * only optimized for hard contrast of dark background;
* Add following configuations to `init.vim`:

```bash
let g:gruvbox_contrast_dark = 'hard'
colorscheme gruvbox
set background=dark
```

#### vim-polyglot

* [sheerun/vim-polyglot](https://github.com/sheerun/vim-polyglot): syntax and indentation support.
* Add following configuations to `init.vim`, and it should insert before the plugin caller:

```bash
" --- disable some languages that already well been colorized --- "
" should call before plugin caller "
let g:polyglot_disabled = [
  \ 'markdown',
  \ ]
```

#### Others

* [vim-smoothie](https://github.com/psliwka/vim-smoothie) helps you chatch up the cursor when moving with `<C-d>` and `<C-u>`;
* [indentLine](https://github.com/Yggdroot/indentLine) helps you read the indentation.

## More Functional Plugins ans Settings

### Git

```bash
Plug 'tpope/vim-fugitive'
```

* [tpope/vim-fugitive](https://github.com/tpope/vim-fugitive) allows you interactive with git in vim command mode without terminal.
* It also helps you recoganize if the current file belongs to a git project and which branch it belongs to if you use statusline like following.

### Statusline and Tabline

* I use `vim-devicons` and `vim-airline` to set up my statusline and tabline.

#### vim-devicons

* [ryanoasis/vim-devicons](https://github.com/ryanoasis/vim-devicons): support a lot of tools to show beautiful icons. It works as long as:
  * [Nerd Font](https://github.com/ryanoasis/nerd-fonts) is installed and has been set as your terminal text font.

#### vim-airline

* [vim-airline/vim-airline](https://github.com/vim-airline/vim-airline): statusline and tabline
* It works with a lot of other plugins, such as `gruvbox`, `vim-devicons`, `fugitive`...
* You can use buffer tabs by setting like this:

```bash
" enable tabline "
let g:airline#extensions#tabline#enabled = 1
let g:airline#extensions#tabline#left_sep = ' '
let g:airline#extensions#tabline#left_alt_sep = '|'
let g:airline#extensions#tabline#right_sep = ' '
let g:airline#extensions#tabline#right_alt_sep = '|'
set showtabline=2       " Always show tabs "
set noshowmode          " We don't need to see things like -- INSERT -- anymore "
" next buffer "
nnoremap  <silent> <S-tab>  :if &modifiable && !&readonly && &modified <CR> :write<CR> :endif<CR>:bnext<CR>
" previous buffer "
nnoremap  <silent> <A-tab>  :if &modifiable && !&readonly && &modified <CR> :write<CR> :endif<CR>:bprevious<CR>
" quit current buffer "
nnoremap  <silent> <A-q>    :bd<CR>
```

### Terminal

* Neovim has integrated terminal, you can set like following:

```bash
tnoremap <Esc> <C-\><C-n>
nnoremap <A-v> :vsplit term://zsh<CR>
nnoremap <A-b> :split term://zsh <bar>resize 5<CR>
```

> remember to replace `zsh` to match your shell.

* However, sometimes I'd like to use [vim-floaterm](https://github.com/voldikss/vim-floaterm).

```bash
Plug 'voldikss/vim-floaterm'

let g:floaterm_complete_options = {'shortcut': 'floaterm', 'priority': 0, 'filter_length': [5, 20]}
nnoremap   <silent>   <F1>    :FloatermNew<CR>
tnoremap   <silent>   <F1>    <C-\><C-n>:FloatermNew<CR>
nnoremap   <silent>   <F7>    :FloatermPrev<CR>
tnoremap   <silent>   <F7>    <C-\><C-n>:FloatermPrev<CR>
nnoremap   <silent>   <F9>    :FloatermNext<CR>
tnoremap   <silent>   <F9>    <C-\><C-n>:FloatermNext<CR>
nnoremap   <silent>   <F12>   :FloatermToggle<CR>
tnoremap   <silent>   <F12>   <C-\><C-n>:FloatermToggle<CR>
```

### Explorer

* There are a lot explorer tools: `coc-explorer`, `netrw`, `nerd-tree`... While I prefer [defx](https://github.com/shougo/defx.nvim) along with its helpers:

```bash
Plug 'Shougo/defx.nvim', { 'do': ':UpdateRemotePlugins' }
Plug 'kristijanhusak/defx-icons'
Plug 'kristijanhusak/defx-git'
```

* To easily manage your plugins, it is recommended to write configuations in a seperated file, `defx.vim` in this case. I set up like following:

```bash
nnoremap <silent> <Leader>e
  \ :<C-U>:Defx -show-ignored-files -resume -split=floating<CR>

autocmd FileType defx call s:defx_my_settings()
function! s:defx_my_settings() abort
  " Define mappings
  nnoremap <silent><buffer><expr> <CR>
  \ defx#is_directory() ?
  \ defx#do_action('open_tree', 'recursive:2') :
  \ defx#do_action('multi', ['drop', 'quit'])
  nnoremap <silent><buffer><expr> v
  \ defx#is_directory() ? 0 : defx#do_action('open', 'vsplit')
  nnoremap <silent><buffer><expr> s
  \ defx#is_directory() ? 0 : defx#do_action('open', 'split')
  nnoremap <silent><buffer><expr> o
  \ match(bufname('%'), 'explorer') >= 0 ?
  \ (defx#is_directory() ? 0 : defx#do_action('drop', 'vsplit')) :
  \ (defx#is_directory() ? 0 : defx#do_action('multi', ['open', 'quit']))
  nnoremap <silent><buffer><expr> l
  \ defx#is_directory() ? defx#do_action('open') : 0
  nnoremap <silent><buffer><expr> h
  \ defx#do_action('cd', ['..'])
  nnoremap <silent><buffer><expr> A
  \ defx#do_action('new_directory')
  nnoremap <silent><buffer><expr> a
  \ defx#do_action('new_file')
  nnoremap <silent><buffer><expr> d
  \ defx#do_action('remove')
  nnoremap <silent><buffer><expr> r
  \ defx#do_action('rename')
  nnoremap <silent><buffer><expr> q
  \ defx#do_action('quit')
endfunction

call defx#custom#option('_', {
  \ 'wincol':&columns / 6,
  \ 'winrow':&lines / 8,
  \ 'winwidth': &columns / 3 * 2,
  \ 'winheight': &lines / 4 * 3,
  \ 'toggle': 1,
  \ 'columns': 'mark:indent:git:icons:filename:type:size:space:time',
  \ })
```

* Don't forget to source int in `init.vim` like following:

```bash
source `~/.config/nvim/defx.vim`
```

### Fuzzy Finder

#### Awesome tools to help you search stuff

* [FZF](https://github.com/junegunn/fzf.vim)
* [ripgrep](https://github.com/BurntSushi/ripgrep)
* [universal-ctags](https://github.com/universal-ctags/ctags)

> You can install them in macOS with following commands:

```bash
brew install fzf

# To install useful key bindings and fuzzy completion:
$(brew --prefix)/opt/fzf/install

brew install ripgrep

brew install --HEAD universal-ctags/universal-ctags/universal-ctags
```

#### Settings for fzf

```bash
Plug 'junegunn/fzf.vim'
Plug 'airblade/vim-rooter'
```

```bash
" This is the default extra key bindings "
let g:fzf_action = {
  \ 'ctrl-t': 'tab split',
  \ 'ctrl-s': 'split',
  \ 'ctrl-v': 'vsplit' }

" Enable per-command history. "
" CTRL-N and CTRL-P will be automatically bound to next-history and "
" previous-history instead of down and up. If you don't like the change, "
" explicitly bind the keys to down and up in your $FZF_DEFAULT_OPTS. "
let g:fzf_history_dir = '~/.local/share/fzf-history'

map <C-f> :Files<CR>
map <leader>b :Buffers<CR>
nnoremap <leader>g :Rg<CR>
nnoremap <leader>t :Tags<CR>
nnoremap <leader>m :Marks<CR>

" Tell fzf to use Ctags "
let g:fzf_tags_command = 'ctags -R'

" Border color "
let g:fzf_layout = {'up':'~90%', 'window': { 'width': 0.8, 'height': 0.8,'yoffset':0.5,'xoffset': 0.5, 'highlight': 'Todo', 'border': 'sharp' } }

let $FZF_DEFAULT_OPTS = '--layout=reverse --info=inline'

" Tell fzf to use ripgrep to show files including the hidden, "
" it will ignore rules in .gitignore by default "
let $FZF_DEFAULT_COMMAND = "rg --files --hidden"

" Customize fzf colors to match your color scheme "
let g:fzf_colors =
\ { 'fg':      ['fg', 'Normal'],
  \ 'bg':      ['bg', 'Normal'],
  \ 'hl':      ['fg', 'Comment'],
  \ 'fg+':     ['fg', 'CursorLine', 'CursorColumn', 'Normal'],
  \ 'bg+':     ['bg', 'CursorLine', 'CursorColumn'],
  \ 'hl+':     ['fg', 'Statement'],
  \ 'info':    ['fg', 'PreProc'],
  \ 'border':  ['fg', 'Ignore'],
  \ 'prompt':  ['fg', 'Conditional'],
  \ 'pointer': ['fg', 'Exception'],
  \ 'marker':  ['fg', 'Keyword'],
  \ 'spinner': ['fg', 'Label'],
  \ 'header':  ['fg', 'Comment'] }

" Get Files "
command! -bang -nargs=? -complete=dir Files
    \ call fzf#vim#files(<q-args>, fzf#vim#with_preview({'options': ['--layout=reverse', '--info=inline']}), <bang>0)

" Get text in files with Rg "
command! -bang -nargs=* Rg
  \ call fzf#vim#grep(
  \   'rg --column --line-number --no-heading --color=always --smart-case '.shellescape(<q-args>), 1,
  \   fzf#vim#with_preview(), <bang>0)

" Ripgrep advanced "
function! RipgrepFzf(query, fullscreen)
  let command_fmt = 'rg --column --line-number --no-heading --color=always --smart-case %s || true'
  let initial_command = printf(command_fmt, shellescape(a:query))
  let reload_command = printf(command_fmt, '{q}')
  let spec = {'options': ['--phony', '--query', a:query, '--bind', 'change:reload:'.reload_command]}
  call fzf#vim#grep(initial_command, 1, fzf#vim#with_preview(spec), a:fullscreen)
endfunction

command! -nargs=* -bang RG call RipgrepFzf(<q-args>, <bang>0)

" Git grep "
command! -bang -nargs=* GGrep
  \ call fzf#vim#grep(
  \   'git grep --line-number '.shellescape(<q-args>), 0,
  \   fzf#vim#with_preview({'dir': systemlist('git rev-parse --show-toplevel')[0]}), <bang>0)
```

* [Note for Extra Keybindings \(Optional\)](https://wiki.archlinux.org/index.php/Fzf)

