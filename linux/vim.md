[linux cheatsheet / vim](linux.md#vim)

# Searching

- To search for a term, type `/SearchTerm`
- To go to the next result, type `N`
- To go to the previous result, type `Shift + N`
- To clear the previous search highlighting, type `:noh`

# Multi-line Editing

Enter visual block mode: `Ctrl + V`

# Read-Only Mode

```bash
vim -R /path/to/file.txt
```

# Commands

```
# Running commands
:/

# Executing commands multiple times (add 2 spaces to top of all lines between 15 and 20)
:15,20 s/^/  /

# Executing commands multiple times (add 2 spaces to top of all lines between 15 and end of file)
:15,$ s/^/  /
```
