# Bash

- [Cheatsheet](#cheatsheet)
- [Resources](#resources)
- [Scripting](#scripting)
- [Keyboard Shortcuts](#keyboard-shortcuts)

## Cheatsheet

- move
  - start: `Ctrl + A`
  - end: `Ctrl + E`
  - back char: `Ctrl + B`
  - back word: `Alt + B`
  - forward char: `Ctrl + F`
  - forward word: `Alt + F`
  - toggle first and current: `Ctrl + XX`
- edit
  - cut next char: `Ctrl + D`
  - cut to start of word: `Ctrl + W`
  - cut to end of word: `Alt + D`
  - cut before cursor: `Ctrl + U`
  - cut after cursor: `Ctrl + K`
  - cut whole line: `Ctrl + A` `Ctrl + K` or `Ctrl + E` `Ctrl + U`
  - paste: `Ctrl + Y`
  - undo: `Ctrl + _`
  - cancel: `Ctrl + C`
  - comment line: `Alt + Shift + #`
- scroll
  - up one line: `Ctrl + Shift + Up`
  - up one page: `Ctrl + Shift + PageUp`
  - down one line: `Ctrl + Shift + Down`
  - down one page: `Ctrl + Shift + PageDown`
- history: `history` or `history 20`
  - reissue last command: `!!` or `sudo !!`
  - reissue command by id: `!1660`
  - previous: `Up` or `Ctrl + P`
  - next: `Down` or `Ctrl + N`
  - end: `Alt + Shift + .`
  - start: `Alt + Shift + ,`
  - search up: `Ctrl + R`
  - search down: `Ctrl + S`
  - select search: `Ctrl + J`
  - cancel search: `Ctrl + G`
  - new empty command: `Ctrl + Alt + >`
- clear terminal: `Ctrl + L`

## Resources

[Linux Cheatsheet](linux.md) or [Linux Quick Reference](quickref.md)

[Bash Reference Manual](https://www.gnu.org/software/bash/manual/bash.html)

[Shell Script Best Practices](https://sharats.me/posts/shell-script-best-practices/)

## Scripting

```bash
# Shift the scripts arguments
shift # $2 becomes $1
shift 2 # $3 becomes $1

# Exit code of last run. '0' if success, '1' if failed.
$?

# To get the assigned value, or default if it's missing:
FOO="${VARIABLE:-default}"  # If variable not set or null, use default.
# If VARIABLE was unset or null, it still is after this (no assignment done).

# Or to assign default to VARIABLE at the same time:
FOO="${VARIABLE:=default}"  # If variable not set or null, set it to default.
```

### Silence Output

```bash
# Silence stdout
command 1> /dev/null
#   or
command > /dev/null

# Silence stderr
command 2> /dev/null

# Send stderr to stdout
command 2>&1

# Silence stdout and stderr (this sends stderr to stdout)
command > /dev/null 2>&1

# Silence stdout and stderr - Bash (>= v4) shortcut
command &> /dev/null
```

## Keyboard Shortcuts

| Action | Keyboard Shortcut |
| --- | --- |
| Move cursor to start of line | `Ctrl + A` |
| Move cursor to end of line | `Ctrl + E` |
| Move back one character | `Ctrl + B` |
| Move back one word | `Alt + B` |
| Move forward one character | `Ctrl + F` |
| Move forward one word | `Alt + F` |
| Toggle between first and current position | `Ctrl + XX` |
| Delete current character | `Ctrl + D` |
| Cut from cursor to start of word | `Ctrl + W` |
| Cut from cursor to end of word | `Alt + D` |
| Cut everything before the cursor | `Ctrl + U` |
| Cut everything after the cursor | `Ctrl + K` |
| Clean up the line | `Ctrl + E` `Ctrl + U` |
| Cancel the command | `Ctrl + C` |
| Paste the last deleted command | `Ctrl + Y` |
| Undo | `Ctrl + _` |
| Save Current Line As Comment | `Alt + Shift + #` |
| Clear the terminal | `Ctrl + L` |
| Search command in history - type the search term | `Ctrl + R` |
| End the search at current history entry | `Ctrl + J` |
| Cancel the search and restore original line | `Ctrl + G` |
| Next command from the History | `Ctrl + N` |
| Previous command from the History | `Ctrl + P` |
| Stop Searching History (Return to Blank Line) | `Ctrl + Alt + >` |
