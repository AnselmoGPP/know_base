# Vim


## Table of contents

+ [References](#references)
+ [Basics](#basics)
+ [Normal mode](#normal-mode)
+ [Help](#help)
+ [Multiple files](#multiple-files)


## References

- [Vi](https://en.wikipedia.org/wiki/Vi_(text_editor)), [Vim](https://en.wikipedia.org/wiki/Vim_(text_editor)), [NeoVim](https://en.wikipedia.org/wiki/Neovim).
- [Learning the Vi and Vim editors, 7th edition (O'Reilly)](https://www.oreilly.com/library/view/learning-the-vi/9780596529833/)
- [Vim as IDE](https://blog.jez.io/vim-as-an-ide/)
- [vim-plug](https://github.com/junegunn/vim-plug)
- [vim + tmux](https://www.youtube.com/watch?v=5r6yzFEXajQ)
- [vim without plugins](https://www.youtube.com/watch?v=XA2WjJbmmoM)
- [nerdtree](https://github.com/scrooloose/nerdtree)
- [Intellisense](https://github.com/neoclide/coc.nvim)
- [Working with multiple files](https://stackoverflow.com/questions/53664/how-to-effectively-work-with-multiple-files-in-vim)
- [Edit multiple files](https://www.ostechnix.com/how-to-edit-multiple-files-using-vim-editor/)
- Cheat sheets:
  - [Rtorr](https://vim.rtorr.com/)
  - [Things Fit Together](https://thingsfittogether.com/)

## Basics

Edit a file:

  - `vim path/to/file.tf`: Open Vim inside your command window
  - `gvim file.tf`: Open Vim in a new window

Vim has a few modes. Move to them when in Normal mode:

- **Normal** (`esc`): Navigation and general modifications
- **Insert** (`i`): Edit file
- **Visual** (`v`): Selection
- **Replace** (`R`): Every typed character deletes an existing one.

Show current mode: `:set showmode`


## Normal mode

Set line's numbers: `:set number`

**Change mode**:

- To **Insert mode**:
  - `i`: Insert mode
  - `A`: Insert mode moving to end of line
  - `a`: Append text after the cursor
  - `o`: Insert line below
  - `O`: Insert line above
- To **Visual mode**:
  - `v`: After selection, you can do different actions, such as:
    - `:w filename`: Save selection in a file
	- `d`: Delete/cut selection
	- `y`: Copy selection
	- `p`: Paste (even if original text was deleted)
- To **Replace mode**: `R`
- Return to **Normal mode**: `esc`

**Quit**:

- `:q`: Quit from Vim
- `:q!`: Quit without saving (also `Ctrl + z + q`)
- `:w`: Save to file
- `:w abc`: Save to file abc
- `:wq`: Save and exit (also `Ctrl + z`)
- `:wq abc`: Save to file abc and close
- `:wq! abc`: Overwrite to file abc and close

**Delete** text:

- `x`: Delete character
- `dw`: Delete word (until next word)
- `d3w`: Delete 3 words
- `de`: Delete word (until word's end)
- `d$`: Delete until end of line
- `dd`: Delete line
- `3dd`: Delete 3 lines

Adding a number before a comand will execute that command that number of times.

**Format** of a command: `operator [number] motion` (example: `d3w, d5$`, `c3e`)

- `operator` : Action to take (`d` [delete], `c` [change], `y` [copy])
- `number`: Optional multiplier for the motion
- `motion`: Where the cursor moves (defines the range) (`w` [word], `e` [end of word], `$` [end of line])

**Cancel** actions:

- `u`: Undo
- `U`: Undo all changes in a line
- `Ctrl + r`: Re-do
- `Esc`: Cancel a partially completed command

**Move**:

- `h`, `j`, `k`, `l`: Left, down, up, right
- `0`: Move to start line
- `w`: Move forward word by word, by beginning of words
- `e`: Move forward word by word, by end of words
- `2w`: Move 2 words forward (until next word)
- `3e`: Move 3 words forward (until word's end)
- `gg`: Go to begin of file
- `G`: Go to end of file
- `55G`: Go to line 55
- `Ctrl + G`: Show position and file status
- `%`: Go to matching (), [], {}

**Retrieve**:

- `:r data`: Retrieve some data and paste it. Examples: `:r myFile`, `:r !ls`.

**Search** "phrase":

- `/phrase`
- `/phrase\c`: Ignore case for just one search
- `?phrase`: Search in backward direction
- `n`: Search again
- `N`: Search again in opposite direction
- `Ctrl + O`: Go back to where you came from
- `Ctrl + I`: Go forward
- `Enter`: Move forward through words
- `Uppercase`: Move backwards
- `:set ic` / `:set noic`: Searching ignores case / Searching doesn't ignore case
- `set hlsearch incsearch`, `:set hls is`: Set `hlsearch` (highlight) and `incsearch` (partial matches) options
- `:nohlsearch`: Remove the highlight of matches (prepend `no` to switch an option off)

**Replace** ABC with XYZ:

- `rx`: Replace character with X (X can be any character)
- `ce`: Replace a word with another (takes you to insert mode)
- `c$`: Replace the rest of the line with another (takes you to insert mode)
- `:s/ABC/XYZ`: First occurrence in the line
- `:s/ABC/XYZ/g`: All occurrences in the line
- `:2,8s/ABC/XYZ/g`: All occurrences between line 2 and 8
- `:%s/ABC/XYZ`: First occurrence in the file
- `:%s/ABC/XYZ/g`: All occurrences in the file
- `:%s/ABC/XYZ/gc`: All accurrences in the files, asking for permission

**External commands**: `:!command` (examples: `:!ls`, `:!rm myFile`)

**Completion**: `Ctrl + D` (vim must not be in compatible mode → `:set nocp`)
  - Shows list of commands starting by X
  - Completes the command name (`:e` → `:edit`) or filename

**vimrc file** (edit it to use more features)

- `:help vimrc-intro`
- `:e ~/.vimrc`: Edit your vimrc
- `:r $VIMRUNTIME/vimrc_example.vim`: Read
- `:w`: Write


## Help

**Help**:

- `:help`
- `:help any-topic`
- `:help user-manual`
- `Ctrl + W`: Jump from window to window
- `:q`: Close help window

**Tutorials**:

- `vimtutor`
- :help user-manual # Ctrl+] (selection), Ctrl+O (jump back)
- :help


## Multiple files

Open multiple files: `vim file1 file2 file3`

Move to next file:

- `:n`, `:next`
- `:wn`, `:wnext`: Saves first
- `:n!`: Doesn't save

Move to previous file:

- `:N`, `:Next`
- `:prev`, `:previous`
- `:wprevious`

Go back to first file: `:rew`

Check on which file you are: `:args`
