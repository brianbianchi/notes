
# VIM

## Cheat sheet

Vim is a powerful text editor that is useful to programmers, system administrators, and heavy editors of plain text files. You are likely to first experience Vim on a linux system or when trying to resolve code conflicts using git. After you read this post, I recommend that you go through the interactive tutorial by typing `vimtutor` into your command line.

The command to edit a file using Vim is `vim filename.type`. There are three main modes to Vim: insert, command, and last-line.

### Command Mode `esc`
When first entering Vim, you begin in command mode. This means that all alphanumeric keys are bound to commands, rather than inserting respective characters.
#### Movements

`h` - one character to the left

`j` - down one line

`k` - up one line

`l` - one character to the right

`0` - to the beginning of the line

`$` - to the end of the line

`w` - forward one word

`b` - backward one word

`G` - to the end of the file

`gg` - to the beginning of the file

`` `. ``  - to the last edit

Prefacing a movement with a number will execute the command that many times. For example, `4j` will move your cursor down four lines.

#### Editing
`x` - delete character

`dw` - deletes from cursor to end of word

`d0` - delete to beginning of a line

`d$` - delete to end of a line

`dgg` - delete to beginning of file

`dG` - delete to end of file

`u` - undo last operation(s)

`Ctrl-r` - redo last undo(s)

#### Search and Replace
`/text` - search for "text", going forward

`n` - move cursor to next instance of searched text (wrapped at end of document)

`N` - move cursor to previous instance of searched text

`?text` - search for "text", going backward

`:%s/text/replacement/g` - search entire document and replace "text" with "replacement"

`:%s/text/replacement/gc` - search entire document and replace "text" with "replacement", with confirmation

#### Copying and Pasting
The last bit of text you deleted is now in your buffer and is ready to be pasted.

`p` - paste text after current line

`P` - paste text on current line

`v` - highlight one character at a time

`V` - highlight one line at a time

`Ctrl-v` - highlight by column

`y` - yank text, after highlighting, place into buffer

### Insert Mode `i`
This mode allows you to insert the respective characters you type on your keyboard. To go back to command mode, use `esc`.

### Last-line Mode `:`
`:q` - quit the editor

`:q!` - override save and quit

`:w {filename}` - write (save) the file

`:ZZ` - save and quit
