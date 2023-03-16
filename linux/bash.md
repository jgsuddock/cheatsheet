# Bash

- [Resources](#resources)
- [Scripting](#scripting)
- [Keyboard Shortcuts](#keyboard-shortcuts)

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
