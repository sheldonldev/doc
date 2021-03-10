# Nvim for Coding

* Based on [Nvim Basic Setup](https://doc.sheldonl.dev/working-env/vim-based-workspace/nvim-basic-setup);
* Complete configurations and features are kept on GitHub:

> I have to say, everyone should have their own settings, while I'll be glad if some of my settings can inspare you.

## Auto-Completion and Snipptes

* There are some auto-completion tools you can use, such as `YouCompleteMe`, `coc.nvim`. I've tried those, finally I stick to `deoplete.nvim`, it can use `nvim-lspconfig` as LSP.
* If you feel you are repeatedly writing code, you need snipptes to helps you auto-complete. I use `ultisnips` as snips engine and use `vim-snippets` as snips repo.

```bash
Plug 'Shougo/deoplete.nvim', { 'do': ':UpdateRemotePlugins' }
Plug 'neovim/nvim-lspconfig',
Plug 'SirVer/ultisnips'
Plug 'honza/vim-snippets'
```

```bash
let g:deoplete#enable_at_startup = 1

" use Tab to scroll, and Enter to select "
inoremap <expr><CR> pumvisible() ? "\<C-y>" : "\<C-g>u\<CR>"
inoremap <expr><Tab> pumvisible() ? "\<C-n>" : "\<Tab>"

nnoremap <silent>gd     <cmd>lua vim.lsp.buf.declaration()<CR>
nnoremap <silent><C-]>  <cmd>lua vim.lsp.buf.definition()<CR>
nnoremap <silent>K      <cmd>lua vim.lsp.buf.hover()<CR>


" === nvim-lspconfig === "
lua <<EOF
require'lspconfig'.html.setup{}
require'lspconfig'.cssls.setup{}
require'lspconfig'.vuels.setup{}
EOF


" === ultisnips === "
" Trigger configuration. You need to change this to something other than <tab> "
let g:UltiSnipsExpandTrigger="<A-l>"
let g:UltiSnipsJumpForwardTrigger="<A-j>"
let g:UltiSnipsJumpBackwardTrigger="<A-k>"
```

## Prettier and Linters

```bash
Plug 'sbdchd/neoformat'
```

## Debugger

## Others

```bash
Plug 'nvim-treesitter/nvim-treesitter'
Plug 'terryma/vim-multiple-cursors'
Plug 'norcalli/nvim-colorizer.lua'
```

