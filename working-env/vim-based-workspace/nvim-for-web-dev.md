# Nvim for Web Dev

- Complete config files are on GitHub:

{% embed url="https://github.com/sheldonldev/nvim_config" caption="My Neovim Config on GitHub" %}

## Install Node

- `npm` provides a lot of tools for web development, such as `browser-sync`.
- We use `coc.nvim` plugin as Language Server, which depends on NodeJS.

So let's install node as well as some global npm packages by following this link:

{% embed url="https://doc.sheldonl.dev/working-env/toolkits/nodejs-and-npm#installation" caption="NodeJS and npm packages Installation" %}

## Install Neovim

- [Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim) (HEAD Version is recommended)

- Edit `~/.config/nvim/init.vim`:

```bash
" load ~/.vimrc and ~/.vim because I use vim before switched to nvim "
set runtimepath^=~/.vim runtimepath+=~/.vim/after
let &packpath = &runtimepath
source ~/.vimrc

" disable python2 because I just want to use python3 "
let g:loaded_python_provider = 0
```

- Run command `:checkhealth` to show more todo list

## Awesome Settings for Neovim

- Awesome settings are kept in `.vimrc`: [Make Vim Awesome](https://doc.sheldonl.dev/working-env/vim-based-workspace/make-vim-awesome).
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

### Plugin Manager

- I use `vim-plug` as plugin manager, following script will install it automatically.

```bash
" auto-install vim-plug "
if empty(glob('~/.vim/autoload/plug.vim'))
  silent !curl -fLo ~/.nvim/autoload/plug.vim --create-dirs
    \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
endif
```

- Append plugins like following in `~/.config/nvim/init.vim`.

```bash
call plug#begin('~/.vim/plugged')
Plug 'venderName/plugName'
Plug 'anotherVender/anotherPlug'
call plug#end()
```

- Run `:w`and `:source %`, then run `:PlugInstall`/`:PlugUpdate`/`:PlugClean`/`:PlugStatus`/`:PlugDiff`.

## Plugin Installation and Settings

### coc.nvim

- This plugin is too featureful to explain: [extensive documentation](https://github.com/neoclide/coc.nvim/wiki).

```bash
Plug 'neoclide/coc.nvim', {'branch': 'release'}
```

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
            \ 'coc-emmet',
            \ 'coc-css',
            \ 'coc-html',
            \ 'coc-json',
            \ 'coc-prettier',
            \ 'coc-tsserver',
            \ 'coc-vetur',
            \ 'coc-python',
            \ 'coc-yaml',
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
  - Here you can add settings for [language servers](https://github.com/neoclide/coc.nvim/wiki/Language-servers)
  - Read more: [using the configuration file](https://github.com/neoclide/coc.nvim/wiki/Using-the-configuration-file)

```json
{
  //eslint,js
  "eslint.trace.server": "verbose",
  "eslint.packageManager": "yarn",
  "prettier.eslintIntegration": true,
  "eslint.autoFix": true,
  "eslint.autoFixOnSave": true,
  "eslint.filetypes": [
    "vue",
    "typescript.tsx",
    "javascript",
    "javascriptreact",
    "typescriptreact",
    "typescript"
  ],
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
  "prettier.tabWidth": 2,
  "prettier.semi": true,
  "prettier.singleQuote": true,
  "prettier.jsxBracketSameLine": true,
  "prettier.jsxSingleQuote": false,
  "prettier.bracketSpacing": true,
  "prettier.trailingComma": "none",
  "prettier.arrowParens": "avoid",
  "prettier.htmlWhitespaceSensitivity": "ignore",
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
  "json.format.enable": true,

  //html
  "html.trace.server": "verbose",
  "html.enable": true,
  "html.format.enable": true,
  "html.validate.html": true,
  "html.validate.styles": true,
  "html.validate.scripts": true,
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
      "singleQuote": false
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
      "rootPatterns": [
        ".ccls",
        "compile_commands.json",
        ".vim/",
        ".git/",
        ".hg/"
      ],
      "initializationOptions": {
        "cache": {
          "directory": "/tmp/ccls"
        }
      }
    }
  },

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

- settings for `coc`:

```bash
" === Explorer === "

autocmd BufEnter * if (winnr("$") == 1 && &filetype == 'coc-explorer') | q | endif
nmap <leader>e :CocCommand explorer<CR>

" Explorer preset "
let g:coc_explorer_global_presets = {
\   '.config/nvim': {
\     'root-uri': '~/.config/nvim',
\   },
\   'hub/doc': {
\     'root-uri': '~/Documents/hub/doc'
\   },
\   'floating': {
\     'position': 'floating',
\     'open-action-strategy': 'sourceWindow',
\   },
\ }

" Use preset argument to open it "
nmap <leader>ef :CocCommand explorer --preset floating<CR>
nmap <leader>ev :CocCommand explorer --preset .config/nvim<CR>
nmap <leader>ed :CocCommand explorer --preset hub/doc<CR>

" List all presets "
nmap <leader>el :CocList explPresets


" === for scss extention === "
autocmd FileType scss setl iskeyword+=@-@


" === for prettier extention === "
command! -nargs=0 Prettier :CocCommand prettier.formatFile
vmap <leader>f  <Plug>(coc-format-selected)
nmap <leader>f  <Plug>(coc-format-selected)


" === for other === "
" Add status line support, for integration with other plugin, checkout `:h coc-status` "
set statusline^=%{coc#status()}%{get(b:,'coc_current_function','')}

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

" Highlight symbol under cursor on CursorHold "
autocmd CursorHold * silent call CocActionAsync('highlight')

" Remap for rename current word "
nmap <leader>rn <Plug>(coc-rename)

augroup mygroup
    autocmd!
    " Setup formatexpr specified filetype(s). "
    autocmd FileType typescript,json setl formatexpr=CocAction('formatSelected')
    " Update signature help on jump placeholder "
    autocmd User CocJumpPlaceholder call CocActionAsync('showSignatureHelp')
augroup end

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

#### Support for Coc Extensions

- `coc-explorer` requires [Nerd Font](https://github.com/ryanoasis/nerd-fonts#font-installation).
- Set your terminal text font to Nerd Font.
- `coc-snippets` can work together with `vim-snippets`, and can use user snippets directory:

  ```bash
  Plug 'honza/vim-snippets'

  " trigger snippet expand. "
  imap <C-l> <Plug>(coc-snippets-expand)

  " select text for visual placeholder of snippet. "
  vmap <C-j> <Plug>(coc-snippets-select)

  " jump to next placeholder, it's default of coc.nvim "
  let g:coc_snippet_next = '<c-j>'

  " jump to previous placeholder, it's default of coc.nvim "
  let g:coc_snippet_prev = '<c-k>'

  " expand and jump (make expand higher priority.) "
  imap <C-j> <Plug>(coc-snippets-expand-jump)
  ```

  ```json
  // add in coc-settings.json to enable user directory
  "snippets.userSnippetsDirectory": "~/.config/nvim/snips"
  ```

- Extensions like `coc-java` can work with [nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter).

  - NOTE: nvim version >= 0.5.0;
  - Add `Plug 'nvim-treesitter/nvim-treesitter'`;
  - Add settings to `init.vim`:

  ```bash
  lua <<EOF
  require'nvim-treesitter.configs'.setup {
    ensure_installed = "maintained", -- one of "all", "maintained" (parsers with maintainers), or a list of languages
    highlight = {
      enable = true,              -- false will disable the whole extension
      disable = { "c", "rust" },  -- list of language that will be disabled
    },
  }
  EOF
  ```

#### More About Coc Extensions

- To check out all extensions: [coc extensions](https://github.com/neoclide/coc.nvim/wiki/Using-coc-extensions). Or run `:CocList marketplace`.
- To manage coc extensions: `:CocList extensions`.
- To find an extension command: `:CocList commands`. For example, you want to create `eslintrc.json`, run `:CocList commands` to check out what commands you can use, then fuzzy finder will help you.
- To run a command: `:CocCommand _command_`, for example, you want to create `eslintrc.json` and find out `eslint.configCreate` can help you, so you run `:CocCommand eslint.configCreate`.
- To uninstall an extension: `:CocUninstall: _extensionName_`.

#### More About Coc Language Suport Commands

- Following is the commonly used commands:

```bash
<Plug>(coc-codeaction)              " line action
<Plug>(coc-definition)              " definition
<Plug>(coc-references)              " references
<Plug>(coc-type-definition)         " type definition
<Plug>(coc-rename)                  " rename
<Plug>(coc-declaration)             " declaration
<Plug>(coc-implementation)          " implementation
<Plug>(coc-format)                  " format
<Plug>(coc-fix-current)             " quickfix
<Plug>(coc-codelens-action)         " code lens
<Plug>(coc-diagnostic-next)         " next diagnostic
<Plug>(coc-diagnostic-next-error)   " next error
:CocList diagnostics                " diagnostics
:CocList outline                    " search outline
:CocList -I symbols                 " references
:CocUpdate                          " update CoC
:CocDisable                         " disable CoC
:CocEnable                          " enable CoC
```

#### More Support for Java

- Install [JDK](https://www.oracle.com/java/technologies/javase-downloads.html);

- Lombok:

```bash
sudo mkdir /usr/local/share/lombok
sudo wget https://projectlombok.org/downloads/lombok.jar -O /usr/local/share/lombok/lombok.jar
```

- `coc-settings.json`:

```bash
// codelens
"codeLens.enable": true,
"java.referencesCodeLens.enabled": true,
"java.jdt.ls.vmargs": "-javaagent:/usr/local/share/lombok.jar",
```

- But still difficult to emplement debugging, find details here: [Java in Neovim](https://www.chrisatmachine.com/Neovim/24-neovim-and-java/)

#### More Support for C/C++

- MacOS run `brew install ccls`.

- To set up a C/C++ project:

  - generate `compile_commands.json` in project root. In macOS, you can use one of the following methods:
    1. Intercepting the system calls and extracting the arguments passed to the compiler by dynamic library injection (e.g. Bear, scan-build):
       - pros: works for hard-coded compiler path;
       - cons: macOS prohibits dynamic library injection for security reasons if the the program to be injected is system software (e.g. clang from Xcode).
    2. Using a compiler wrapper (e.g. scan-build):
       - pros: doesn’t violate security policies;
       - cons: the compiler path must not be hard-coded.
  - place `.ccls` in project root. It is a text file, in which each line is a command line argument passed to the compiler. Here is an example:

    ```text
    -I
    ../include
    -I
    ../vendor/include
    -std=c++14
    -stdlib=libc++
    -fPIC
    ```

- If `ccls` cannot find your system headers…

  - If you are using macOS, then chances are `ccls` cannot find system headers and as a result reports a bunch of errors.
  - This is because new macOS systems moves system headers into the macOS SDK directory and no longer places them in `/usr/include`.
  - To solve this problem, you can manually adding the path of the system headers to `.ccls`:

    - Run `g++ -E -x c++ - -v < /dev/null` in your terminal and you’ll see a list of include paths that the compiler searches.
    - They are between `#include <...> search starts here:` and End of search list..
    - Now put them into your `.ccls` file as `-isystem` options:
      - unlike `-I`, the errors and warnings in the header files found in `-isystem` paths are ignored by the syntax checker.
    - After manually adding these system header paths, the `.ccls` file might look like this:

      ```text
      -isystem
      /usr/local/include
      -isystem
      /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/include/c++/v1
      -isystem
      /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/lib/clang/10.0.1/include
      -isystem
      /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/include
      -isystem
      /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.14.sdk/usr/include
      ```

### gruvbox

- I prefer `gruvbox` as theme.

```bash
" repo: https://github.com/morhetz/gruvbox "
Plug 'morhetz/gruvbox'

" settings "
colorscheme gruvbox
set background=dark
```

### polyglot

- I prefer `polyglot` to color code.

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

- I prefer `airline` to show the status line.

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

### Fuzzy Finder

#### Awesome tools to help you search stuff

- [FZF](https://github.com/junegunn/fzf.vim)
- [ripgrep](https://github.com/BurntSushi/ripgrep)
- [universal-ctags](https://github.com/universal-ctags/ctags)

You can install them in macOS with following commands:

```bash
brew install fzf

# To install useful key bindings and fuzzy completion:
$(brew --prefix)/opt/fzf/install

brew install ripgrep

brew install --HEAD universal-ctags/universal-ctags/universal-ctags
```

#### Nvim settings for fzf and ripgrep

```bash
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
Plug 'junegunn/fzf.vim'

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

## References

- [Chris@Machine/neovim](https://www.chrisatmachine.com/neovim)
- [devilyouwei/Vimmer](https://github.com/devilyouwei/Vimmer)
- [Configure coc.nvim for C/C++ Development](https://ianding.io/2019/07/29/configure-coc-nvim-for-c-c++-development/)
- [ThePrimeagen - Your first VimRC: How to setup your vim's vimrc](https://www.youtube.com/watch?v=n9k9scbTuvQ)
