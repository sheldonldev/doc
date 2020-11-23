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

```bash
" nerdtree, https://github.com/preservim/nerdtree "
Plug 'preservim/nerdtree'

" airline also, https://github.com/vim-airline/vim-airline "
Plug 'vim-airline/vim-airline'
```

-   NERDTree settings

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

### Fuzzy Finder & Git Manager

#### fzf

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

### Language Support

#### coc.nvim

-   This plugin is too featureful (bloated) to explain. Good thing is the author provided
    [extensive documentation](https://github.com/neoclide/coc.nvim/wiki)

```bash
Plug 'neoclide/coc.nvim', {'branch': 'release'}
```

-   The config will be long, so let's keep it in a seperate file `$HOME/.config/nvim/plug-config/coc.vi` and tell
    `init.vim` to do so.

```bash
source ~/.config/nvim/plug-config/coc.vim
```

-   Check coc health:

    -   there should be an entry for `coc`
    -   use `g:coc_node_path` to point to your node
    -   run `CocInfo` to get more info.

-   Install more coc extensions:
    -   To checkout all extentions: [coc extensions](https://github.com/neoclide/coc.nvim/wiki/Using-coc-extensions).
    -   To manage coc extensions: `:CocList extensions`.
    -   To find an extention command: `:CocList commands`, where fuzzy finder will help you find the command you want if
        you have installed it. For example, you want to create `eslintrc.json`, run `:CocList commands` to checkout what
        commands you can use, then fuzzy finder will help you
    -   To run a command: `:CocCommand _command_`, for example, you want to create `eslintrc.json` and find out
        `eslint.configCreate` can help you, then you just run `:CocCommand eslint.configCreate`, everything will be
        done.
    -   To Uninstall an enstention: `:CocUninstall: _extensionName_`.

```bash
" Install by adding this config or by running `:CocInstall _extensionName_`"
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
            \ 'coc-stylelint',
            \ 'coc-snippets',
            \ 'coc-highlight',
            \ 'coc-phpls',
            \ 'coc-wxml',
            \ 'coc-java',
            \ 'coc-omnisharp',
            \ 'coc-angular'
            \ ]
```

-   Language Server Configuration:
    -   Run `:CocConfig` will open `~/.config/nvim/coc-settings.json`.
    -   Here you can add [language servers](https://github.com/neoclide/coc.nvim/wiki/Language-servers)
    -   Read more [using the configuration file](https://github.com/neoclide/coc.nvim/wiki/Using-the-configuration-file)

```json
{
    //eslint,js
    "eslint.trace.server": "verbose",
    "eslint.packageManager": "yarn",
    "prettier.eslintIntegration": true,
    "eslint.autoFix": true,
    "eslint.autoFixOnSave": true,
    "eslint.filetypes": ["vue", "typescript.tsx", "javascript", "javascriptreact", "typescriptreact", "typescript"],
    "eslint.run": "onSave",

    //tsserver
    //use eslint to check js and ts
    "tsserver.trace.server": "verbose",
    "javascript.validate.enable": false,
    "typescript.validate.enable": false,
    "eslint.options": { "configFile": ".eslintrc.json" },

    //emmet
    "emmet.priority": 1,
    "emmet.excludeLanguages": ["vue"],

    //prettier
    "prettier.useTabs": false,
    "prettier.tabWidth": 4,
    "prettier.semi": false,
    "prettier.singleQuote": true,
    "prettier.jsxBracketSameLine": true,
    "prettier.printWidth": 120,
    "prettier.jsxSingleQuote": false,
    "prettier.bracketSpacing": true,
    "prettier.trailingComma": "none",
    "prettier.arrowParens": "avoid",
    "prettier.htmlWhitespaceSensitivity": "ignore",
    "prettier.proseWrap": "always",
    "coc.preferences.formatOnSaveFiletypes": [
        "javascript",
        "typescript",
        "typescriptreact",
        "json",
        "javascriptreact",
        "typescript.tsx",
        "css",
        "markdown"
    ],

    //json
    "json.format.enable": false,

    //html
    "html.trace.server": "verbose",
    "html.enable": true,
    "html.format.enable": true,
    "html.validate.html": true,
    "html.validate.styles": true,
    "html.validate.scripts": true,
    "html.format.wrapLineLength": 100,
    "html.format.endWithNewline": false,
    "html.format.wrapAttributes": "auto",

    //vue
    "vetur.trace.server": "verbose",
    "vetur.format.enable": true,
    "vetur.validation.style": true,
    "vetur.validation.script": true,
    "vetur.validation.template": true,
    "vetur.format.defaultFormatterOptions": {
        "prettyhtml": {
            "sortAttributes": true,
            "singleQuote": false,
            "printWidth": 120
        }
    },
    "vetur.format.defaultFormatter.js": "prettier-eslint",
    "vetur.format.defaultFormatter.html": "prettier",
    "vetur.format.defaultFormatter.css": "prettier",
    "vetur.format.defaultFormatter.less": "prettier",
    "vetur.format.defaultFormatter.scss": "prettier",
    "vetur.format.defaultFormatter.ts": "prettier-tslint",
    "vetur.format.defaultFormatter.stylus": "stylus-supremacy",
    "vetur.format.defaultFormatter.postcss": "prettier",

    // java
    "java.trace.server": "verbose",
    "java.errors.incompleteClasspath.severity": "ignore",

    // c/c++
    "languageserver": {
        "ccls": {
            "command": "ccls",
            "filetypes": ["c", "cpp", "objc", "objcpp"],
            "rootPatterns": [".ccls", "compile_commands.json", ".vim/", ".git/", ".hg/"],
            "initializationOptions": {
                "cache": {
                    "directory": "/tmp/ccls"
                }
            }
        }
    }
}
```

-   `coc` settings:

```bash
" for scss extention "
autocmd FileType scss setl iskeyword+=@-@

" for prettier extention "
command! -nargs=0 Prettier :CocCommand prettier.formatFile
vmap <leader>f  <Plug>(coc-format-selected)
nmap <leader>f  <Plug>(coc-format-selected)
" Prettier range format only support languageId including: "
" javascript, javascriptreact, typescript, typescriptreact, json and graphql. "

" for python extention "
set statusline^=%{coc#status()}
" if you need lint: `pip3 install pylint`"

" Use tab for trigger completion with characters ahead and navigate.
" Use command ':verbose imap <tab>' to make sure tab is not mapped by other plugin.
inoremap <silent><expr> <TAB>
      \ pumvisible() ? "\<C-n>" :
      \ <SID>check_back_space() ? "\<TAB>" :
      \ coc#refresh()
inoremap <expr><S-TAB> pumvisible() ? "\<C-p>" : "\<C-h>"

function! s:check_back_space() abort
  let col = col('.') - 1
  return !col || getline('.')[col - 1]  =~# '\s'
endfunction

" Use <CR> to confirm completion, `<C-g>u` means break undo chain at current position.
" Coc only does snippet and additional edit on confirm.
inoremap <expr> <cr> pumvisible() ? "\<C-y>" : "\<C-g>u\<CR>"

" Use `[c` and `]c` to navigate diagnostics
nmap <silent> [c <Plug>(coc-diagnostic-prev)
nmap <silent> ]c <Plug>(coc-diagnostic-next)

" Remap keys for gotos
nmap <silent> gd <Plug>(coc-definition)
nmap <silent> gy <Plug>(coc-type-definition)
nmap <silent> gi <Plug>(coc-implementation)
nmap <silent> gr <Plug>(coc-references)

" Use K to show documentation in preview window
nnoremap <silent> K :call <SID>show_documentation()<CR>

function! s:show_documentation()
  if (index(['vim','help'], &filetype) >= 0)
    execute 'h '.expand('<cword>')
  else
    call CocAction('doHover')
  endif
endfunction

" Highlight symbol under cursor on CursorHold
autocmd CursorHold * silent call CocActionAsync('highlight')

" Remap for rename current word
nmap <leader>rn <Plug>(coc-rename)

" Remap for format selected region
xmap <leader>f  <Plug>(coc-format-selected)
nmap <leader>f  <Plug>(coc-format-selected)

augroup mygroup
  autocmd!
  " Setup formatexpr specified filetype(s).
  autocmd FileType typescript,json setl formatexpr=CocAction('formatSelected')
  " Update signature help on jump placeholder
  autocmd User CocJumpPlaceholder call CocActionAsync('showSignatureHelp')
augroup end

" Remap for do codeAction of selected region, ex: `<leader>aap` for current paragraph
xmap <leader>a  <Plug>(coc-codeaction-selected)
nmap <leader>a  <Plug>(coc-codeaction-selected)

" Remap for do codeAction of current line
nmap <leader>ac  <Plug>(coc-codeaction)
" Fix autofix problem of current line
nmap <leader>qf  <Plug>(coc-fix-current)

" Use <tab> for select selections ranges, needs server support, like: coc-tsserver, coc-python
nmap <silent> <TAB> <Plug>(coc-range-select)
xmap <silent> <TAB> <Plug>(coc-range-select)
xmap <silent> <S-TAB> <Plug>(coc-range-select-backword)

" Use `:Format` to format current buffer
command! -nargs=0 Format :call CocAction('format')

" Use `:Fold` to fold current buffer
command! -nargs=? Fold :call     CocAction('fold', <f-args>)

" use `:OR` for organize import of current buffer
command! -nargs=0 OR   :call     CocAction('runCommand', 'editor.action.organizeImport')

" Add status line support, for integration with other plugin, checkout `:h coc-status`
set statusline^=%{coc#status()}%{get(b:,'coc_current_function','')}

" Using CocList
" Show all diagnostics
nnoremap <silent> <A-a>  :<C-u>CocList diagnostics<cr>
" Manage extensions
nnoremap <silent> <A-e>  :<C-u>CocList extensions<cr>
" Show commands
nnoremap <silent> <A-c>  :<C-u>CocList commands<cr>
" Find symbol of current document
nnoremap <silent> <A-o>  :<C-u>CocList outline<cr>
" Search workspace symbols
nnoremap <silent> <A-s>  :<C-u>CocList -I symbols<cr>
" Do default action for next item.
nnoremap <silent> <A-j>  :<C-u>CocNext<CR>
" Do default action for previous item.
nnoremap <silent> <A-k>  :<C-u>CocPrev<CR>
" Resume latest coc list
nnoremap <silent> <A-p>  :<C-u>CocListResume<CR>
```
