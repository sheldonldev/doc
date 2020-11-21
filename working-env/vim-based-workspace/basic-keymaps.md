# Basic Keymaps

| **Key**            | **Map**                                                                   |
| :----------------- | :------------------------------------------------------------------------ |
| `h: key-notation`  | key notation manual.                                                      |
| -                  | -                                                                         |
| `i`                | insert before the cursor.                                                 |
| `I`                | insert at the start of the line.                                          |
| `a`                | append after the cursor.                                                  |
| `A`                | append at the end of the line.                                            |
| `o`                | open a new line above.                                                    |
| `O`                | open a new line below.                                                    |
| -                  | -                                                                         |
| `x`                | cut the current char.                                                     |
| `X`                | cut the char before the cursor.                                           |
| `s`                | cut the current char and insert.                                          |
| `S`                | cut the current line and insert.                                          |
| `r`                | replace the current char.                                                 |
| `R`                | replace chars afterward until exit the replace mode.                      |
| `~`                | reverse upper/lower case.                                                 |
| `dd`               | cut the current line.                                                     |
| `yy`               | yank the current line.                                                    |
| `cc`               | change the current line, the same as `S`.                                 |
| `p`                | paste below the line.                                                     |
| `P`                | paste above the line.                                                     |
| -                  | -                                                                         |
| `j`, `k`, `h`, `l` | move up, down, left, right.                                               |
| `<CR>`             | move the cursor to the start of the next line.                            |
| `gg`/`[[`          | move the cursor to the top of the file.                                   |
| `G`/`]]`           | move the cursor to the bottom of the file.                                |
| `_n_G`/`:_n_`      | move the cursor to _n_-th line.                                           |
| `^`                | move the cursor to the start of the line, after whitespace.               |
| `0`                | move the cursor to the start of the line.                                 |
| `$`                | move the cursor to the end of line.                                       |
| `w`                | move the cursor a word forward.                                           |
| `W`                | move the cursor a word forward, skip punctuation.                         |
| `e`                | move the cursor to word end.                                              |
| `E`                | move the cursor to word end, including punctuation.                       |
| `b`                | move the cursor a word backward.                                          |
| `B`                | move the cursor a word backward, skip punctuation.                        |
| `H`                | move the cursor to the top of the screen.                                 |
| `L`                | move the cursor to the bottom of the screen.                              |
| `M`                | move the cursor to the middle of the screen.                              |
| `f_c_`             | find char _c_ forward in the line.                                        |
| `F_c_`             | find char _c_ backward in the line.                                       |
| `t_c_`             | to until char _c_ forward in the line.                                    |
| `T_c_`             | to until char _c_ backward in the line.                                   |
| `;`                | next `f`/`F`/`t`/`T` result.                                              |
| `,`                | prev `f`/`F`/`t`/`T` result.                                              |
| `{`                | move the cursor above the paragraph.                                      |
| `}`                | move the cursor to the end of the paragraph.                              |
| `(`                | move the cursor to the start of the sentence.                             |
| `)`                | move the cursor to the end of then sentence.                              |
| -                  | -                                                                         |
| `ygg`              | yank the current line and all above.                                      |
| `yG`               | yank the current line and all below.                                      |
| `y_n_G`            | yank the current line and above/below till _n_-th line.                   |
| `y0`               | yank content span the cursor and the start of the line.                   |
| `y^`               | yank content span the cursor and the start of the line before whitespace. |
| `y$`               | yank content span the cursor and the end of the line.                     |
| `yw`               | yank the current word.                                                    |
| `yW`               | yank the current word and punctuation.                                    |
| `yb`               | yank the chars before the cursor of this word, cursor included.           |
| `yB`               | yank the chars before the cursor of this word, cursor excluded.           |
| `c<?>`, `d<?>`     | similar to `y<?>`.                                                        |
| `_n_<?>`           | repeate command _n_ times, for example `3w`.                              |
| `.`                | repeate command.                                                          |
| -                  | -                                                                         |
| `>>`               | indent current line.                                                      |
| `<<`               | unindent current line.                                                    |
| `J`                | join the next line to the current line.                                   |
| -                  | -                                                                         |
| `u`                | undo.                                                                     |
| `U`                | undo line.                                                                |
| `<C-r>`            | redo.                                                                     |
| -                  | -                                                                         |
| `<C-e>`            | scroll the screen up.                                                     |
| `<C-y>`            | scroll the screen down.                                                   |
| `<C-d>`            | scroll a half page down.                                                  |
| `<C-f>`            | scroll a full page down.                                                  |
| `<C-u>`            | scroll a half page up.                                                    |
| `<C-b>`            | scroll a full page up.                                                    |
| `zz`               | scroll the current line to the middle of the screen.                      |
| -                  | -                                                                         |
| `:/_str_<CR>`      | search _str_ from current to top.                                         |
| `N`                | search last one.                                                          |
| `:%s/foo/bar/gci`  | search and replace, globally, with confirmation, case insensitive.        |
| `:noh`             | no highlighting.                                                          |
| `*`                | search next identifier of the current word.                               |
| `#`                | search prev identifier of the current word.                               |
| `K`                | search current word in manual.                                            |
| -                  | -                                                                         |
| `m_m_`             | set mark _m_, good practice: `mh`, `mj`, `mk`, `ml`.                      |
| `'_m_`             | goto mark _m_ line.                                                       |
| `<Backtick>_m_`    | goto mark _m_ cursor.                                                     |
| `<C-o>`            | goto prev mark.                                                           |
| -                  | -                                                                         |
| `:w`               | save.                                                                     |
| `:wa`              | save all changed files in the buffer.                                     |
| `:q`               | quit.                                                                     |
| `:qa`              | quit all.                                                                 |
| `:wq`/`ZZ`         | save and quit.                                                            |
| `:q!`              | quit but not save.                                                        |
| `<C-z>`            | suspend and back to shell.                                                |
| `v`                | visual mode. You can manipulate with `y`, `d`, `c`, `<`, `>`...           |
| `V`                | visual line mode. You can manipulate with `y`, `d`, `c`, `<`, `>`...      |
| `<C-v>`            | visual block mode. You can edit multi-lines in this mode!                 |
| `<Esc>`/`<C-c>`    | exit current mode.                                                        |
