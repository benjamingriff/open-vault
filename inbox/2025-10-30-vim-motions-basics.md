---
id: 2025-10-30-vim-motions-basics
aliases: []
tags: []
---

# Basic Neovim Commands

## Movement
*   `h`: Move cursor left
*   `j`: Move cursor down
*   `k`: Move cursor up
*   `l`: Move cursor right
*   `w`: Move to the next word
*   `b`: Move to the beginning of the word
*   `0` (zero): Move to the beginning of the line
*   `$`: Move to the end of the line
*   `gg`: Move to the beginning of the file
*   `G`: Move to the end of the file
*   `:n` then press Enter: Go to line number `n` (e.g., `:10` to go to line 10)

## Editing
*   `i`: Insert before the cursor
*   `a`: Append after the cursor
*   `o`: Open a new line below the current line and enter insert mode
*   `O`: Open a new line above the current line and enter insert mode
*   `x`: Delete the character under the cursor
*   `dd`: Delete the entire line
*   `yy`: Yank (copy) the entire line
*   `p`: Paste after the cursor
*   `P`: Paste before the cursor
*   `r`: Replace the character under the cursor (e.g., `ra` replaces with 'a')
*   `u`: Undo the last change
*   `Ctrl + r`: Redo the last undone change
*   `.` (dot): Repeat the last command

## Visual Mode
*   `v`: Enter visual mode (character-wise selection)
*   `V`: Enter visual mode (line-wise selection)
*   `Ctrl + v`: Enter visual block mode (column-wise selection)
*   In visual mode:
    *   Use movement keys (`h`, `j`, `k`, `l`, `w`, `b`, etc.) to select text.
    *   `d`: Delete the selected text
    *   `y`: Yank (copy) the selected text
    *   `>`: Indent the selected text
    *   `<`: Unindent the selected text

## Saving and Exiting
*   `:w`: Save the file
*   `:q`: Quit Neovim (if no changes have been made)
*   `:wq` or `:x`: Save the file and quit
*   `:q!`: Quit Neovim without saving (discard changes)
*   `:w new_file_name`: Save the file as `new_file_name`

## Search
*   `/pattern`: Search forward for `pattern`
*   `?pattern`: Search backward for `pattern`
*   `n`: Find the next occurrence of the pattern
*   `N`: Find the previous occurrence of the pattern

## Other Useful Commands
*   `:help command`: Open the help documentation for `command` (e.g., `:help dd`)
*   `:set number`: Show line numbers
*   `:set nonumber`: Hide line numbers

## Combining Commands (Examples)
*   `dw`: Delete word
*   `ciw`: Change inner word (delete the word under the cursor and enter insert mode)
*   `3dd`: Delete 3 lines
*   `yyp`: Duplicate the current line

This is just a starting point. Neovim is very powerful and customizable, so explore more commands and configurations as you get more comfortable!
