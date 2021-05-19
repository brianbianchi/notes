
# VIM cheat sheet

### Movement

`h` - one character to the left

`j` - down one line

`k` - up one line

`l` - one character to the right

`0` - to the beginning of the line

`$` - to the end of the line

`w` - forward one word

`b` - backward one word

`fx` – jump to next occurrence of character x

`tx` - jump to before next occurrence of character x

`}` – jump to next paragraph (or function/block, when editing code)

`{` – jump to previous paragraph (or function/block, when editing code)

`G` - to the end of the file

`gg` - to the beginning of the file

`i` - inner  (`di{` deletes everything in {})

`a` - outer (`da{` deletes {} and everything in it)

`` `. ``  - to the last edit

Prefacing a movement with a number will execute the command that many times. For example, `4j` will move your cursor down four lines.

### Editing
`x` - delete character

`c` - change

`d` - delete

`v` - select

`u` - undo last operation(s)

`Ctrl-r` - redo last undo(s)

### Search and Replace
`/text` - search for "text", going forward

`n` - move cursor to next instance of searched text (wrapped at end of document)

`N` - move cursor to previous instance of searched text

`?text` - search for "text", going backward

`:%s/text/replacement/g` - search entire document and replace "text" with "replacement"

`:%s/text/replacement/gc` - search entire document and replace "text" with "replacement", with confirmation

### Copying and Pasting
The last bit of text you deleted is now in your buffer and is ready to be pasted.

`p` - paste text after current line

`P` - paste text on current line

`v` - highlight one character at a time

`V` - highlight one line at a time

`Ctrl-v` - highlight by column

`y` - yank text, after highlighting, place into buffer

### Insert Mode `i`
`i` - insert before cursor

`a` - insert after cursor

`o` - new line after

`O` - new line before

`ea` - insert at the end of the word

### Last-line Mode `:`
`:q` - quit the editor

`:q!` - override save and quit

`:w {filename}` - write (save) the file

`:ZZ` - quit and save

`:ZQ` - quit without saving
