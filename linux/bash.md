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

[Linux Cheatsheet](linux.md)

[Bash Reference Manual](https://www.gnu.org/software/bash/manual/bash.html)

[Shell Script Best Practices](https://sharats.me/posts/shell-script-best-practices/)

## Scripting

```bash
# Conditionals

-n
   string is not null.

-z
  string is null, that is, has zero length

[ -n "$foo" ]

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

- conditionals:
  - `-a file`: True if file exists.
  - `-b file`: True if file exists and is a block special file.
  - `-c file`: True if file exists and is a character special file.
  - `-d file`: True if file exists and is a directory.
  - `-e file`: True if file exists.
  - `-f file`: True if file exists and is a regular file.
  - `-g file`: True if file exists and its set-group-id bit is set.
  - `-h file`: True if file exists and is a symbolic link.
  - `-k file`: True if file exists and its "sticky" bit is set.
  - `-p file`: True if file exists and is a named pipe (FIFO).
  - `-r file`: True if file exists and is readable.
  - `-s file`: True if file exists and has a size greater than zero.
  - `-t fd`: True if file descriptor fd is open and refers to a terminal.
  - `-u file`: True if file exists and its set-user-id bit is set.
  - `-w file`: True if file exists and is writable.
  - `-x file`: True if file exists and is executable.
  - `-G file`: True if file exists and is owned by the effective group id.
  - `-L file`: True if file exists and is a symbolic link.
  - `-N file`: True if file exists and has been modified since it was last read.
  - `-O file`: True if file exists and is owned by the effective user id.
  - `-S file`: True if file exists and is a socket.
  - `file1 -ef file2`: True if file1 and file2 refer to the same device and inode numbers.
  - `file1 -nt file2`: True if file1 is newer (according to modification date) than file2, or if file1 exists and file2 does not.
  - `file1 -ot file2`: True if file1 is older than file2, or if file2 exists and file1 does not.
  - `-o optname`: True if the shell option optname is enabled. The list of options appears in the description of the -o option to the set builtin (see The Set Builtin).
  - `-v varname`: True if the shell variable varname is set (has been assigned a value).
  - `-R varname`: True if the shell variable varname is set and is a name reference.
  - `-z string`: True if the length of string is zero.
  - `-n string`: True if the length of string is non-zero.
  - `string1 -eq string2` or `string1 = string2`: True if the strings are equal.
  - `string1 -ne string2` or `string1 != string2`: True if the strings are not equal.
  - `string1 -lt string2` or `string1 < string2`: True if string1 sorts before string2 lexicographically.
  - `string1 -le string2`: True if string1 sorts before string2 lexicographically or if the strings are equal.
  - `string1 -gt string2` or `string1 > string2`: True if string1 sorts after string2 lexicographically.
  - `string1 -ge string2`: True if string1 sorts after string2 lexicographically or if the strings are equal.

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
