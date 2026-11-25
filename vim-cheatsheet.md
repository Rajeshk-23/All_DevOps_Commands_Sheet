# Vim Cheatsheet

> A practical reference for Vim modes, navigation, editing, search, and workflow commands.

## Table of Contents
- [Modes](#modes)
- [Movement](#movement)
- [Editing](#editing)
- [Insert Mode](#insert-mode)
- [Visual Mode](#visual-mode)
- [Copy & Paste](#copy--paste)
- [Search & Replace](#search--replace)
- [Files & Buffers](#files--buffers)
- [Windows & Tabs](#windows--tabs)
- [Marks & Macros](#marks--macros)
- [Miscellaneous](#miscellaneous)

## Modes

| Keystroke | Description |
| --- | --- |
| `Esc` | Return to Normal mode. |
| `i` | Insert before the cursor. |
| `a` | Insert after the cursor. |
| `v` | Enter characterwise Visual mode. |
| `V` | Enter linewise Visual mode. |
| `Ctrl-v` | Enter blockwise Visual mode. |
| `:` | Enter Command-line mode. |
| `R` | Enter Replace mode. |
| `Ctrl-o` | Execute one Normal-mode command from Insert mode. |

## Movement

| Keystroke | Description |
| --- | --- |
| `h` | Move left. |
| `j` | Move down. |
| `k` | Move up. |
| `l` | Move right. |
| `w` | Move to the start of the next word. |
| `b` | Move to the start of the previous word. |
| `e` | Move to the end of the current or next word. |
| `0` | Move to the first column. |
| `^` | Move to the first non-blank character. |
| `$` | Move to the end of the line. |
| `gg` | Move to the first line. |
| `G` | Move to the last line. |
| `5G` | Move to line five. |
| `Ctrl-d` | Scroll down half a screen. |
| `Ctrl-u` | Scroll up half a screen. |
| `%` | Jump between matching brackets. |

## Editing

| Keystroke | Description |
| --- | --- |
| `x` | Delete the character under the cursor. |
| `dd` | Delete the current line. |
| `D` | Delete from the cursor to the end of the line. |
| `dw` | Delete through the next word. |
| `diw` | Delete the word under the cursor. |
| `d$` | Delete to the end of the line. |
| `cc` | Replace the current line and enter Insert mode. |
| `C` | Change from the cursor to the end of the line. |
| `r{char}` | Replace one character. |
| `J` | Join the current line with the next line. |
| `u` | Undo the last change. |
| `Ctrl-r` | Redo the last undone change. |
| `.` | Repeat the last change. |

## Insert Mode

| Keystroke | Description |
| --- | --- |
| `i` | Insert before the cursor. |
| `I` | Insert at the first non-blank character. |
| `a` | Append after the cursor. |
| `A` | Append at the end of the line. |
| `o` | Open a new line below and insert. |
| `O` | Open a new line above and insert. |
| `s` | Delete the character and insert. |
| `S` | Replace the line and insert. |
| `Ctrl-w` | Delete the previous word while inserting. |
| `Ctrl-u` | Delete back to the start of the inserted line. |
| `Esc` | Leave Insert mode. |

## Visual Mode

| Keystroke | Description |
| --- | --- |
| `v` | Select characters under the cursor. |
| `V` | Select whole lines. |
| `Ctrl-v` | Select a rectangular block. |
| `o` | Move to the opposite selection corner. |
| `O` | Move to the opposite block-selection corner. |
| `d` | Delete the selected text. |
| `c` | Change the selected text. |
| `y` | Yank the selected text. |
| `>` | Indent the selection. |
| `<` | Unindent the selection. |
| `~` | Toggle case for the selection. |
| `gv` | Reselect the previous Visual selection. |

## Copy & Paste

| Keystroke | Description |
| --- | --- |
| `yy` | Yank the current line. |
| `yw` | Yank through the next word. |
| `y$` | Yank from the cursor to the line end. |
| `p` | Put text after the cursor or line. |
| `P` | Put text before the cursor or line. |
| `"ayy` | Yank the current line into register `a`. |
| `"ap` | Put text from register `a`. |
| `:reg` | List the contents of registers. |
| `ddp` | Move the current line down one position. |
| `"+y` | Yank to the system clipboard when supported. |
| `"+p` | Paste from the system clipboard when supported. |

## Search & Replace

| Keystroke | Description |
| --- | --- |
| `/pattern` | Search forward for a pattern. |
| `?pattern` | Search backward for a pattern. |
| `n` | Jump to the next search match. |
| `N` | Jump to the previous search match. |
| `*` | Search forward for the word under the cursor. |
| `#` | Search backward for the word under the cursor. |
| `:noh` | Clear search highlighting. |
| `:%s/old/new/g` | Replace every match in the current file. |
| `:%s/old/new/gc` | Replace every match with confirmation. |
| `:s/old/new/` | Replace the first match on the current line. |
| `:g/pattern/d` | Delete every line matching a pattern. |
| `:v/pattern/d` | Delete every line not matching a pattern. |

## Files & Buffers

| Command | Description |
| --- | --- |
| `:edit file` | Open a file in the current buffer. |
| `:enew` | Create an empty buffer. |
| `:write` | Save the current file. |
| `:write file` | Save the buffer to a new file. |
| `:update` | Save only when the buffer has changed. |
| `:quit` | Quit the current window. |
| `:wq` | Save and quit. |
| `:q!` | Quit without saving changes. |
| `:e!` | Reload the file and discard buffer changes. |
| `:files` | List open and alternate files. |
| `:bnext` | Switch to the next buffer. |
| `:bprevious` | Switch to the previous buffer. |
| `:buffer 3` | Switch to buffer number three. |
| `:bdelete` | Delete the current buffer. |

## Windows & Tabs

| Keystroke | Description |
| --- | --- |
| `:split file` | Open a file in a horizontal split. |
| `:vsplit file` | Open a file in a vertical split. |
| `Ctrl-w h` | Move to the window on the left. |
| `Ctrl-w j` | Move to the window below. |
| `Ctrl-w k` | Move to the window above. |
| `Ctrl-w l` | Move to the window on the right. |
| `Ctrl-w q` | Close the current window. |
| `Ctrl-w =` | Equalize window dimensions. |
| `Ctrl-w +` | Increase the current window height. |
| `Ctrl-w >` | Increase the current window width. |
| `:tabnew file` | Open a file in a new tab. |
| `gt` | Move to the next tab. |
| `gT` | Move to the previous tab. |
| `:tabclose` | Close the current tab. |

## Marks & Macros

| Keystroke | Description |
| --- | --- |
| `ma` | Set mark `a` at the cursor. |
| `` `a `` | Jump to the exact position of mark `a`. |
| `'a` | Jump to the first non-blank character on mark `a`'s line. |
| `:marks` | List available marks. |
| `qa` | Record keystrokes into register `a`. |
| `q` | Stop recording a macro. |
| `@a` | Execute the macro in register `a`. |
| `@@` | Repeat the last executed macro. |
| `:normal @a` | Execute macro `a` across a selected range. |

## Miscellaneous

| Command | Description |
| --- | --- |
| `:set number` | Show absolute line numbers. |
| `:set relativenumber` | Show relative line numbers. |
| `:set nowrap` | Disable line wrapping. |
| `:set paste` | Adjust options for inserting pasted text. |
| `:syntax on` | Enable syntax highlighting. |
| `:help topic` | Open built-in help for a topic. |
| `:version` | Display the Vim version and features. |
| `:!command` | Run an external command from Vim. |
| `:r !command` | Insert external command output below the cursor. |
| `zz` | Center the current line on screen. |
| `z=` | Show spelling suggestions for the word under the cursor. |
