# Basic Keymaps

__Key__ | __Map__
-|-
`h: key-notation` | key notation manual.
-|-
`i` | insert before the cursor.
`I` | insert at the beginning of the current line.
`a` | append after the cursor.
`A` | append at the end of the current line.
`o` | open a new line above the current line.
`O` | open a new line below the current line.
-|-
`x` | cut the current char.
`X` | cut the char before the cursor.
`s` | cut the current char and insert.
`S` | cut the current line and insert.
`r` | replace the current char.
`R` | replace chars afterward until exit the replace mode.
`~` | reverse upper/lower case.
`dd` | cut the current line.
`yy` | yank the current line.
`cc` | change the current line, same as `S`.
`p` | paste after the current line.
`P` | paste before the current line.
-|-
`j`, `k`, `h`, `l` | move up, down, left, right.
`<CR>` | move the cursor to the beginning of the next line.
`gg`/`[[` | move the cursor to the top of the file.
`G`/`]]` | move the cursor to the bottom of the file.
`_n_G`/`:_n_` | move the cursor to the _n_th line.
`^`/`0` | move the cursor to the beginning of the current line.
`$` | move the cursor to the end of the current line.
`w` | move the cursor a word forward.
`W` | move the cursor a word forward, skip punctuation.
`e` | move the cursor to word end.
`B` | move the cursor a word backward, skip punctuation.
`H` | move the cursor to the top of the screen.
`L` | move the cursor to the bottom of the screen.
`M` | move the cursor to the middle of the screen.
`f_c_` | find forward on char _c_ in the line.
`F_c_` | find backward on char _c_ in the line.
`t_c_` | forward until char _c_ in the line.
`T_c_` | backward until char _c_ in the line.
`;` | next `f`/`F`/`t`/`T` result.
`,` | prev `f`/`F`/`t`/`T` result.
`{` | move the cursor above the paragraph.
`}` | move the cursor to the end of the paragraph.
`(` | move the cursor to the beginning of the sentence.
`)` | move the cursor to the end of the sentence.
-|-
`ygg` | yank current line and all above.
`yG` | yank current line and all below.
`y_n_G` | yank current line and above/below till the _n_th line.
`y0` | yank content between the cursor and the start of the line (ends included).
`y$` | yank content between the cursor and the end of the line (ends included).
`yw` | yank the current word.
`yW` | yank the current word along with the punctuation.
`yb` | yank the chars before the cursor of this word, cursor included.
`yB` | yank the chars before the cursor of this word, cursor excluded.
`c<?>`, `d<?>` | similar to `y<?>`.
`_n_<?>` | repeate command _n_ times, for example `3w`.
`.` | repeate command.
-|-
`>>` | indent current line.
`<<` | undent current line.
`J` | join next line to the current line.
-|-
`u` | undo.
`U` | undo line.
`<C-r>` | redo.
-|-
`<C-e>` | scroll the screen up.
`<C-y>` | scroll the screen down.
`<C-d>` | scroll a half page down.
`<C-f>` | scroll a full page down.
`<C-u>` | scroll a half page up.
`<C-b>` | scroll a full page up.
`zz` | scroll the current line to the middle of the screen.
-|-
`:/_str_<CR>` | search _str_ from top.
`:?_str_<CR>` | search _str_ from current line.
`n` | search next one.
`N` | search last one.
`:%s/foo/bar/gci` | search and replace, globally, with confirmation, case insensitive. `y(es)`/`n(o)`/`replace (a)ll`/`(q)uit`/`rep(l)ace`/`<C-e>`/`<C-y>`.
`:noh` | no highlighting.
`*` | search next identifier of the current word.
`#` | search prev identifier of the current word.
`K` | search current word in manual
-|-
`m_m_` | set mark _m_, good practice: `mh`, `mj`, `mk`, `ml`.
`'_m_` | goto mark _m_ line.
`<Grave_accent>_m_` | goto mark _m_ cursor.
`<C-o>` | goto prev mark.
-|-
`:!_command_` | run a shell command.
`:w` | save.
`:q` | quit.
`:wq`/`ZZ` | save and quit.
`:q!` | quit without save.
`<C-z>` | suspend and back to shell.
`v` | visual mode. You can manipulate with `y`, `d`, `c`, `<`, `>`...
`V` | visual line mode. You can manipulate with `y`, `d`, `c`, `<`, `>`...
`<C-v>` | visual block mode. You can edit multi-lines in this mode!
`<Esc>`/`<C-c>`| exit current mode.
