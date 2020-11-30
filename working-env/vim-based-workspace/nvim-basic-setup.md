# Nvim Basic Setup

## Install Node

- `npm` provides a lot of tools for web development, such as `live-server`.
- We use `coc.nvim` plugin as Language Server, which depends on NodeJS.

> You can install node and some global npm packages by following this instruction:

{% embed url="https://doc.sheldonl.dev/working-env/toolkits/nodejs-and-npm" caption="NodeJS and npm" %}

## Install Neovim

- [Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim) (HEAD Version is recommended)

- Edit `~/.config/nvim/init.vim`:

```bash
" load ~/.vimrc and ~/.vim because I use vim before switched to nvim "
set runtimepath^=~/.vim runtimepath+=~/.vim/after
let &packpath = &runtimepath
source ~/.vimrc
```

- Run command `:checkhealth` to show more todo list.

## Awesome Settings for Neovim

- Based on `.vimrc`: [Make Vim Awesome](https://doc.sheldonl.dev/working-env/vim-based-workspace/make-vim-awesome).

### Integrated Terminal

```bash
" turn terminal to normal mode with escape "
tnoremap <Esc> <C-\><C-n>

" open terminal on ctrl+n "
function! OpenTerminal()
    split term://zsh          " I use zsh "
    resize 5
endfunction
nnoremap <C-n> :call OpenTerminal()<CR>
```

## Simple Plugins for Startup

### Tools Plugins May Depend On

- Some plugins require [Nerd Font](https://github.com/ryanoasis/nerd-fonts) to show icons.

### Plugin Manager

- Install plugin manager: [vim-plug](https://github.com/junegunn/vim-plug).

> Add following script to `init.vim` and run `:w`and `:source %` will help you install it automatically.

```bash
" auto-install vim-plug "
if empty(glob('~/.vim/autoload/plug.vim'))
  silent !curl -fLo ~/.nvim/autoload/plug.vim --create-dirs
    \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
endif
```

### Install Some Simple Plugins

- Now you can append plugins like the following to `init.vim`. the plugins' names are the names of their git repositories:

```bash
call plug#begin('~/.vim/plugged')
Plug 'morhetz/gruvbox'
Plug 'vim-airline/vim-airline'

Plug 'tpope/vim-commentary'
Plug 'tpope/vim-surround'

Plug 'sheerun/vim-polyglot'
call plug#end()
```

- Run `:w`and `:source %`, then run `:PlugInstall`/`:PlugUpdate`/`:PlugClean`/`:PlugStatus`/`:PlugDiff`.

- Now you should read the documentation in the repositories to set up your plugins. The following are examples.

### Example Settings

#### vim-polyglot

- [sheerun/vim-polyglot](https://github.com/sheerun/polyglot)

```bash
" --- disable some languages that already well been colorized --- "
" should call before plugin caller "
let g:polyglot_disabled = [
  \ 'markdown',
  \ ]
```

#### gruvbox

- [morhetz/gruvbox](https://github.com/morhetz/gruvbox):

```bash
colorscheme gruvbox
set background=dark
```

#### vim-airline

- [vim-airline/vim-airline](https://github.com/vim-airline/vim-airline):

```bash
" enable tabline "
let g:airline#extensions#tabline#enabled = 1
let g:airline#extensions#tabline#left_sep = ' '
let g:airline#extensions#tabline#left_alt_sep = '|'
let g:airline#extensions#tabline#right_sep = ' '
let g:airline#extensions#tabline#right_alt_sep = '|'

set showtabline=2       " Always show tabs "
set noshowmode          " We don't need to see things like -- INSERT -- anymore "
```

#### vim-commentary

- [tpope/vim-commentary](https://github.com/tpope/vim-commentary):

```bash
nnoremap <leader>/ :Commentary<CR>
vnoremap <leader>/ :Commentary<CR>
```

#### vim-surround

- [tpope/vim-surround](https://github.com/tpope/vim-surround):
  - quickly change surrounding pairs or tags;
  - `h: surround`

## More Complex Plugins

### Fuzzy Finder

#### Awesome tools to help you search stuff

- [FZF](https://github.com/junegunn/fzf.vim)
- [ripgrep](https://github.com/BurntSushi/ripgrep)
- [universal-ctags](https://github.com/universal-ctags/ctags)

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
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
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

- [Note for Extra Keybindings (Optional)](https://wiki.archlinux.org/index.php/Fzf)

### coc.nvim

- This plugin is too featureful to explain: [extensive documentation](https://github.com/neoclide/coc.nvim/wiki).

- Install: `Plug 'neoclide/coc.nvim', {'branch': 'release'}`

- The config will be long, so let's keep it in a separate file `~/.config/nvim/coc.vim` and tell `init.vim` to source.

```bash
source ~/.config/nvim/coc.vim
```

- Check coc health:

  - there should be an entry for `coc`;
  - use `g:coc_node_path` to point to your node;
  - run `CocInfo` to get more info.

- Install more coc extensions:

```bash
let g:coc_global_extensions = [
            \ 'coc-marketplace',
            \ 'coc-explorer',
            \ ]
```

- Language Server Configuration:
  - Run `:CocConfig` will open `~/.config/nvim/coc-settings.json`.
  - Add settings for [language servers](https://github.com/neoclide/coc.nvim/wiki/Language-servers) and other plugins

```json
{
  // explorer
  "explorer.width": 25,
  "explorer.icon.enableNerdfont": true,
  "explorer.previewAction.onHover": false,
  "explorer.file.showHiddenFiles": true,
  "explorer.keyMappings.global": {
    "<cr>": ["expandable?", "expand", "open"],
    "v": "open:vsplit"
  }
}
```

> Read more: [using the configuration file](https://github.com/neoclide/coc.nvim/wiki/Using-the-configuration-file)

- settings for `coc`:

```bash
" === Explorer === "

autocmd BufEnter * if (winnr("$") == 1 && &filetype == 'coc-explorer') | q | endif
nmap <leader>e :CocCommand explorer<CR>

" Explorer preset "
let g:coc_explorer_global_presets = {
\   'floating': {
\     'position': 'floating',
\     'open-action-strategy': 'sourceWindow',
\     'floating-width': -50
\   },
\ }

" Use preset argument to open it "
nmap <leader>ef :CocCommand explorer --preset floating<CR>
nmap <leader>ev :CocCommand explorer --preset floating ~/.config/nvim<CR>
nmap <leader>ed :CocCommand explorer --preset floating ~/Documents/hub/doc<CR>

" List all presets "
nmap <leader>el :CocList explPresets


" === Remaps === "

" Use tab for trigger completion with characters ahead and navigate. "
" Use command ':verbose imap <tab>' to make sure tab is not mapped by other plugin. "
inoremap <silent><expr> <TAB>
      \ pumvisible() ? "\<C-n>" :
      \ <SID>check_back_space() ? "\<TAB>" :
      \ coc#refresh()
inoremap <expr><S-TAB> pumvisible() ? "\<C-p>" : "\<C-h>"

function! s:check_back_space() abort
    let col = col('.') - 1
    return !col || getline('.')[col - 1]  =~# '\s'
endfunction

" Use <CR> to confirm completion, `<C-g>u` means break undo chain at current position. "
" Coc only does snippet and additional edit on confirm. "
inoremap <expr> <cr> pumvisible() ? "\<C-y>" : "\<C-g>u\<CR>"

" Use `[c` and `]c` to navigate diagnostics "
nmap <silent> [c <Plug>(coc-diagnostic-prev)
nmap <silent> ]c <Plug>(coc-diagnostic-next)

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

" Remap for rename current word "
nmap <leader>rn <Plug>(coc-rename)

" Remap for do codeAction of selected region, ex: `<leader>aap` for current paragraph "
xmap <leader>a  <Plug>(coc-codeaction-selected)
nmap <leader>a  <Plug>(coc-codeaction-selected)

" Remap for do codeAction of current line "
nmap <leader>ac  <Plug>(coc-codeaction)
" Fix autofix problem of current line "
nmap <leader>qf  <Plug>(coc-fix-current)

" Use <tab> for select selections ranges, needs server support, like: coc-tsserver, coc-python "
nmap <silent> <TAB> <Plug>(coc-range-select)
xmap <silent> <TAB> <Plug>(coc-range-select)
xmap <silent> <S-TAB> <Plug>(coc-range-select-backword)

" Use `:Format` to format current buffer "
command! -nargs=0 Format :call CocAction('format')

" Use `:Fold` to fold current buffer "
command! -nargs=? Fold :call     CocAction('fold', <f-args>)

" use `:OR` for organize import of current buffer "
command! -nargs=0 OR   :call     CocAction('runCommand', 'editor.action.organizeImport')
```

#### More About Coc Extensions

- To check out all extensions: [coc extensions](https://github.com/neoclide/coc.nvim/wiki/Using-coc-extensions). Or run `:CocList marketplace`.
- To manage coc extensions: `:CocList extensions`.
- To find an extension command: `:CocList commands`. For example, you want to create `eslintrc.json`, run `:CocList commands` to check out what commands you can use, then fuzzy finder will help you.
- To run a command: `:CocCommand _command_`, for example, you want to create `eslintrc.json` and find out `eslint.configCreate` can help you, so you run `:CocCommand eslint.configCreate`.
- To uninstall an extension: `:CocUninstall: _extensionName_`.

#### More About Coc Language Suport Commands

```bash
<Plug>(coc-codeaction)              " line action "
<Plug>(coc-definition)              " definition "
<Plug>(coc-references)              " references "
<Plug>(coc-type-definition)         " type definition "
<Plug>(coc-rename)                  " rename "
<Plug>(coc-declaration)             " declaration "
<Plug>(coc-implementation)          " implementation "
<Plug>(coc-format)                  " format "
<Plug>(coc-fix-current)             " quickfix "
<Plug>(coc-codelens-action)         " code lens "
<Plug>(coc-diagnostic-next)         " next diagnostic "
<Plug>(coc-diagnostic-next-error)   " next error "
:CocList diagnostics                " diagnostics "
:CocList outline                    " search outline "
:CocList -I symbols                 " references "
:CocUpdate                          " update CoC "
:CocDisable                         " disable CoC "
:CocEnable                          " enable CoC "
```

### nvim-treesitter

- [nvim-treesitter/nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter):

- This is a basic language support for a lot of languages, the syntax highlight is much beautiful than vim-polyglot, but some languages are not perfect because its still developing.

```bash
Plug 'nvim-treesitter/nvim-treesitter'
```

- The settings is a little different because it is written in `lua`.

  - `~/.config/nvim/lua/treesitter.lua`

  ```lua
  require'nvim-treesitter.configs'.setup {
    ensure_installed = "maintained", -- one of "all", "maintained" (parsers with maintainers), or a list of languages
    highlight = {
      enable = true,        -- false will disable the whole extension
      disable = {},         -- list of language that will be disabled
    },
  }
  ```

  - source config in `init.vim`:

  ```bash
  lua require'treesitter'
  ```

- Run `:h nvim-treesitter` to checkout the usage.

## References

- [Chris@Machine/neovim](https://www.chrisatmachine.com/neovim)
- [devilyouwei/Vimmer](https://github.com/devilyouwei/Vimmer)
