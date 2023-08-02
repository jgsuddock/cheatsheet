- [Cheatsheet](#cheatsheet)
- [Searching](#searching)
- [Multi-line Editing](#multi-line-editing)
- [Read-Only Mode](#read-only-mode)
- [Commands](#commands)

## Cheatsheet

- read-only: `vim -R file.txt` or `view file.txt`
- panes
  - split horizontally: `:split`
  - split vertically: `:vsplit`
  - switch panes: `Ctrl + W` + `J` (direction)
- command mode
  - repeat: `.`
  - undo: `u`
  - redo: `Ctrl + R`
  - insert mode: `I`
    - edit start of line: `Shift + I`
    - edit end of line: `Shift + A`
  - visual mode: `V`
  - visual block mode: `Ctrl + V`
  - decrease indent: `<<`
  - increase indent: `>>`
  - run shell command: `:!ls /dir`
- search
  - start: `/SearchTerm`
  - next: `N`
  - previous: `Shift + N`
  - clear: `:noh`
- replace
  - next in line: `:s/SearchTerm/ReplaceTerm`
  - next in file: `:%s/SearchTerm/ReplaceTerm`
  - to replace all: use `/g` at end
  - to confirm: use `/c` at end
- .vimrc

```
set tabstop=2 shiftwidth=2 expandtab smarttab autoindent number mouse=n list listchars=lead:·,trail:·,tab:»␣
hi SpecialKey ctermfg=DarkGray
```

## Searching

- To search for a term, type `/SearchTerm`
- To go to the next result, type `N`
- To go to the previous result, type `Shift + N`
- To clear the previous search highlighting, type `:noh`

## Multi-line Editing

Enter visual block mode: `Ctrl + V`

## Read-Only Mode

```bash
vim -R /path/to/file.txt
```

## Other Commands

```
# Running commands
:/

# Executing commands multiple times (add 2 spaces to top of all lines between 15 and 20)
:15,20 s/^/  /

# Executing commands multiple times (add 2 spaces to top of all lines between 15 and end of file)
:15,$ s/^/  /
```
