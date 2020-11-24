# Nvim for Web Dev

- References:
  - [Chris@Machine/neovim](https://www.chrisatmachine.com/neovim)
- Complete config files are on GitHub:

{% embed url="https://github.com/sheldonldev/nvim_config" caption="My Neovim Config on GitHub" %}

## Install Node

- `npm` provides a lot of tools for web development, such as `browser-sync`.
- We use `coc.nvim` plugin as Language Server Protocol, which depends on NodeJS.

So let's install node as well as some global npm packages by following this link:

{% embed url="https://doc.sheldonl.dev/working-env/toolkits/nodejs-and-npm#installation" caption="NodeJS and npm packages Installation" %}

## Install Neovim

```bash
brew install neovim

mkdir ~/.config/nvim
touch ~/.config/nvim/init.vim
```

- Edit `~/.config/init.vim`:

```bash
" load ~/.vimrc and ~/.vim because I use vim before switched to nvim "
set runtimepath^=~/.vim runtimepath+=~/.vim/after
let &packpath = &runtimepath
source ~/.vimrc

" disable python2 because I just want to use python3"
let g:loaded_python_provider = 0
```

- Run command `:checkhealth` to show more todo list

## Awesome Settings for Neovim

- Awesome settings are kept in `.vimrc`:
  [Make Vim Awsome](https://doc.sheldonl.dev/working-env/vim-based-workspace/make-vim-awesome)
- Following settings can only be used in Neovim.

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

## Install Plugin Manager

- I use `vim-plug` as plugin manager

```bash
# repo: https://github.com/junegunn/vim-plug
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

- Append plugins like following in `~/.config/nvim/init.vim`

```bash
call plug#begin('~/.vim/plugged')
Plug 'venderName/plugName'
Plug 'anotherVender/anotherPlug'
call plug#end()
```

- Run `:w`and `:source %`, then run `:PlugInstall`/`:PlugUpdate`/`:PlugClean`/`:PlugStatus`/`:PlugDiff`

## Plugin Installation and Settings

### coc.nvim

- This plugin is too featureful to explain: [extensive documentation](https://github.com/neoclide/coc.nvim/wiki)

```bash
Plug 'neoclide/coc.nvim', {'branch': 'release'}
```

- The config will be long, so let's keep it in a seperate file `~/.config/nvim/coc.vi` and tell `init.vim` to do so.

```bash
source ~/.config/nvim/coc.vim
```

- Check coc health:

  - there should be an entry for `coc`
  - use `g:coc_node_path` to point to your node
  - run `CocInfo` to get more info.

- Install more coc extensions:
  - To checkout all extentions: [coc extensions](https://github.com/neoclide/coc.nvim/wiki/Using-coc-extensions).
  - To manage coc extensions: `:CocList extensions`.
  - To find an extention command: `:CocList commands`, where fuzzy finder will help you find the command you want if you
    have installed it. For example, you want to create `eslintrc.json`, run `:CocList commands` to checkout what
    commands you can use, then fuzzy finder will help you
  - To run a command: `:CocCommand _command_`, for example, you want to create `eslintrc.json` and find out
    `eslint.configCreate` can help you, then you just run `:CocCommand eslint.configCreate`, everything will be done.
  - To Uninstall an enstention: `:CocUninstall: _extensionName_`.
  - To show all diagnostics: `:CocList diagnostics`.
  - Find symbol of current document: `:CocList outline`.
  - Search workspace symbols: `:CocList -I symbols`.
  - Do default action to next or prev: `:CocNext`, `:CocPrev`.
  - Resume latest CocList: `CocListResume`.

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
            \ 'coc-java',
            \ 'coc-explorer',
            \ 'coc-marketplace'
            \ ]
```

- Language Server Configuration:
  - Run `:CocConfig` will open `~/.config/nvim/coc-settings.json`.
  - Here you can add [language servers](https://github.com/neoclide/coc.nvim/wiki/Language-servers)
  - Read more [using the configuration file](https://github.com/neoclide/coc.nvim/wiki/Using-the-configuration-file)

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
    "emmet.excludeLanguages": [],

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

    // explorer
    "explorer.width": 30,
    "explorer.icon.enableNerdfont": true,
    "explorer.previewAction.onHover": false,
    "explorer.keyMappings.global": {
        "<cr>": ["expandable?", "expand", "open"],
        "v": "open:vsplit"
    }

    // snippets
    "snippets.userSnippetsDirectory": "~/.config/nvim/snips",
}
```

- `coc` settings:

```bash
" Explorer preset"
let g:coc_explorer_global_presets = {
\   '.vim': {
\     'root-uri': '~/.vim',
\   },
\   'floating': {
\     'position': 'floating',
\     'open-action-strategy': 'sourceWindow',
\   },
\ }

" Explorer "
autocmd BufEnter * if (winnr("$") == 1 && &filetype == 'coc-explorer') | q | endif
nmap <C-e> :CocCommand explorer<CR>

" Use preset argument to open it "
nmap <C-f> :CocCommand explorer --preset floating<CR>
nmap <leader>ev :CocCommand explorer --preset .vim<CR>


" for scss extention "
autocmd FileType scss setl iskeyword+=@-@

" for prettier extention "
command! -nargs=0 Prettier :CocCommand prettier.formatFile
vmap <leader>f  <Plug>(coc-format-selected)
nmap <leader>f  <Plug>(coc-format-selected)
" Prettier range format only support languageId including: "
" javascript, javascriptreact, typescript, typescriptreact, json and graphql. "

" if you need lint for py3: `pip3 install pylint`"

" Add status line support, for integration with other plugin, checkout `:h coc-status`
set statusline^=%{coc#status()}%{get(b:,'coc_current_function','')}

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

```

#### Dependencies for Coc Extensions

- `coc-explorer` requires [Nerd Font](https://github.com/ryanoasis/nerd-fonts#font-installation), please set your
  terminal text font to Nerd Font.
- `coc-snippets` can work together with `vim-snippets` or can use user snippets directory:

```bash
Plug 'honza/vim-snippets'

" Use <C-l> for trigger snippet expand.
imap <C-l> <Plug>(coc-snippets-expand)

" Use <C-j> for select text for visual placeholder of snippet.
vmap <C-j> <Plug>(coc-snippets-select)

" Use <C-j> for jump to next placeholder, it's default of coc.nvim
let g:coc_snippet_next = '<c-j>'

" Use <C-k> for jump to previous placeholder, it's default of coc.nvim
let g:coc_snippet_prev = '<c-k>'

" Use <C-j> for both expand and jump (make expand higher priority.)
imap <C-j> <Plug>(coc-snippets-expand-jump)
```

```json
// coc-settings.json
"snippets.userSnippetsDirectory": "~/.config/nvim/snips"
```

### gruvbox

- I prefer `gruvbox` as my theme.

```bash
" repo: https://github.com/morhetz/gruvbox "
Plug 'morhetz/gruvbox'

" settings "
colorscheme gruvbox
set background=dark
```

### polyglot

- I prefer `polyglot` to color my code.

```bash
" disable the filetypes that you don't want to be colorized by polyglot before call the plug "
let g:polyglot_disabled = [
            \'css',
            \'cs',
            \'markdown',
            \'reactjavascript',
            \'reacttypescript',
            \'php'
            \]

" call plugin "
Plug 'sheerun/vim-polyglot'
```

### airline

- I prefer `airline` to show status line.

```bash
" airline also, https://github.com/vim-airline/vim-airline "
Plug 'vim-airline/vim-airline'
```

### vim-commentary

```bash
Plug 'tpope/vim-commentary'

nnoremap <C-/> :Commentary<CR>
vnoremap <C-/> :Commentary<CR>
```

### vim-rainbow

```bash
Plug 'frazrepo/vim-rainbow'

let g:rainbow_active = 1
let g:rainbow_load_separately = [
    \ [ '*.json', [['\[', '\]'], ['{', '}']] ],
    \ [ '*.{c,cpp,java,js,ts,py,php,sh,css,scss}' , [['(', ')'], ['\[', '\]'], ['{', '}']] ],
    \ [ '*.{html,htm,vue,jsx}' , [['(', ')'], ['\[', '\]'], ['{', '}'], ['<\a[^>]*>', '</[^>]*>']] ],
    \ ]
```

### Fuzzy Finder

- [fzf.vim](https://github.com/junegunn/fzf.vim)

```bash
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
Plug 'junegunn/fzf.vim'
```

- `fzf` settings:

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
