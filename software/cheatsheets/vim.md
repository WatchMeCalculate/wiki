Vim
===


## Open Files
 - Open existing file in new buffer `:e <file>`
 - Open new file in horizontal split window `:new`
 - Open new file in vertical split window `:vnew`
 - Open new file in current window `:enew`

## Save Files
 - Save all files `:wa`
 - Save current file as new file `:saveas <file>`

## Buffers
 - List buffers `:ls`
 - Close current buffer `:bd`
 - Go to next `:bn`
 - Go to prev `:bp`

## Tabs
 - Move tab `:tabm <value>` ex: `relative: -1, +3 absolute: 2`

## Deletions
 - Delete line from cursor to end `D`
 - Delete whole line and be in insert mode `S`

## Text Selection
 - Select current word under cursor `viw`
 - Select everything inside a block `vib`
 - Select everything inside a {/[/( `vi{/[/(`

## Paste
 - Paste from a different buffer `"<buffer number>p`

## Text Navigation
 - Move to first non-blank character of line `_`
 - Move to last non-blank character of line `g_`
 - Jump between last two positions `''` beginning of line, ``` `` ``` will go to last cursor position
 - Set mark on current cursor position `m<some letter>` uppercase will denote between files
 - Go back to mark beginning of line `'<letter>` or where mark cursor was set `` `<letter> ``
 - see marks `:marks`

## File Browser
### Open
 - Open file browser in current window `:Ex`
 - Open file browser in split h windows `:Sex`
 - Open file browser in split h windows `:Vex`
 - Open file browser in new tab `:Tex`
### Inside
 - Change view mode `i` normal / compact list / tree
 - Create directory `d`
 - Create new file `%`
 - Delete file or directory `D`
 - Rename file or directory `R`

## External command
 - Run external command `:! <command> ` adding `%` at end for current file
 - Run external command and save output to buffer `:r ! <command>`

## In Practice useful operations
### Comment out / Uncomment code
#### Comment out
1. `ctrl-v` -> visual block mode
2. select lines
3. `shift + I` -> insert mode
4. add what characters you want
5. press `esc`

#### Comment In
1. `ctrl-v` -> visual block mode
2. select lines
3. use arrows to select text, `shift <-/->` selects chunks
5. press `d` or `x` to delete



