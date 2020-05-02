# Vim

## Normal Mode

- `i` go to insert Mode
- `x` delete character, `X` delete backward, `3x` -> delete 3 character
- `r` replace this character with next one -> wait for next character
- `o` open new line below and go to insert mode, `O` open new line Above
- `a` append to the end and go insert mode
- `u` undo
- `d` delete , `dw` delete one word, `dd` delete one line
- `J` join two line (add next line to this line)
- `G` goto line, `10G` goto line 10, `G` goto last line
- `y` yank (copy), `yy` copy this line, `yw` copy word
- `p` paste in the next line, `P` paste in above
- `/` go to search, `n` next, `N` previous
- `$` end of line, `d$` delete to end of line
- `^` start of line
- `.` repeat last command
- `:` command , `:w` write (save), `:wq` write and quite, `:q!` quite without save
- `%` go to end or start of this bracket or parentheses
- `v` go to visual mode - select span

## Insert Mode

- `esc` back to normal mode

# Visual mode

- `it` select inner tag in html - only content of tag
- `ot` select outer tag in html - tag and content in it
- select some line + `shift + >` => tab to right
- select some line + `:sort` => sort selected line
- select some line + `:normal A;` => all semicolon at the end of selected line

# Command mode

- start with `:`, show intellisense with tab
- `set number` show line number
- `set nonumber` hide line number
- `set outoindent`
- `colorschema desert`
- `set paste` -> ready for paste something
- `Explor` -> open file manager
- `Vexplor` -> file manager in half of page (vertical)
- `Sexplor` -> file manager in half of page (horizontal)
- `ctrl + w + arrow` -> move between split page
- `!` run os command -> `:!ls`
- `!!` run and write the output in file
- `ls` buffer list (list of file in buffer - if you open multi file)

### buffer

- if you open multi file, you see first and other go to buffer
- `bn` go to next buffer
- `bp` go to previous buffer
- `b1` go to buffer number 1
- `b life` go to buffer with life in the name of that
- `bd` delete current buffer, `bd!` delete anyway

- `/world` find first world in file
- `s/a/b/` replace first a with b, `s/a/b/g` replace all a in line with b
- `18,37s/word/the_word` replace from line 18 to line 37 word with the_word
- `%s/word/the_word/` replace in all file
- `18,37/^/\/\//` add // start of lines from 18 to 37

# link

- [vim tutor](http://www2.geog.ucl.ac.uk/~plewis/teaching/unix/vimtutor) it's text file can open in vim and learn vim
- [vim adventures](https://vim-adventures.com/) game for learn vim
