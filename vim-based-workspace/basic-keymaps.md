# Basic Keymaps

__Key__ | __Map__
-|- 
`h: key-notation` | key notation manual
-|-
`:!_command_` | run a shell command
`:w` | save
`:q` | quit
`:wq`/`ZZ` | save and quit
`:q!` | quit without save
`v` | visual mode by cursor
`V` | visual mode by line
`<C-v>` | visual mode by block
`<Esc>`/`<C-c>`| exit current mode
-|-
`i` | insert before cursor
`I` | insert at the beginning of the current line
`a` | append after cursor
`A` | append at the end of the current line
`o` | open new line above the current line
`O` | open new line below the current line
-|-
`x` | cut the char under the cursor
`X` | cut the char before the cursor
`dd` | cut the current line
`yy` | yank the current line
`cc` | cut the current line and insert
`p` | paste after the current line
`P` | paset before the current line
-|-
`j`, `k`, `h`, `l` | move up, down, left, right
`gg`/`[[` | move cursor to the top of the file
`G`/`]]` | move cursor to the bottom of the file
`_n_G`/`:_n_` | move cursor to the _nth_ line
`0` | move cursor to the beginning of the current line
`$` | move cursor to the end of the current line
`w` | move cursor a word forward
`W` | move cursor a word forward, skip punctuation
`e` | move cursor to word end
`B` | move cursor a word backward, skip punctuation
`H` | move cursor to the top of the screen
`L` | move cursor to the bottom of the screen
`M` | move cursor to the middle of the screen
`t_char_` | move cursor to the char before _char_
`{` | move cursor above the paragraph
`}` | move cursor to then end of the paragraph
-|-
`ygg` | yank current line and all above
`yG` | yank current line and all below
`y_n_G` | yank current linet and above/below till the _nth_ line
`y0` | yank content between the cursor and the start of the line (ends included)
`y$` | yank content between the cursor and the end of the line (ends included)
`yw` | yank the current word 
`yW` | yank the current word along with the punctuation
`yb` | yank the chars before the cursor of this word, cursor included
`yB` | yank the chars before the cursor of this word, cursor excluded
`c?`, `d?` | similar to `y?`
-|-
`u` | undo
`U` | undo line
`<C-r>` | redo
-|-
`<C-e>` | scroll the screen up
`<C-y>` | scroll the screen down
`<C-d>` | scroll half page down
`<C-f>` | scroll full page down
`<C-u>` | scroll half page up
`<C-b>` | scroll full page up
`zz` | scroll the current line to the middle of the screen
-|-
`:/_str_<CR>` | search _str_
`n` | search next one
`N` | search last one
`:%s/foo/bar/gci` | search and replace, globally, with confirmation, case insensitive. `y(es)`/`n(o)`/`replace (a)ll`/`(q)uit`/`rep(l)ace`/`<C-e>`/`<C-y>`
-|-
`m_m_` | set mark _m_, such as `mh`, `mj`, `mk`, `ml`... 
`\`_m` | goto mark _m_ 
