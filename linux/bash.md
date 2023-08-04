# Bash

- [Resources](#resources)
- [Keyboard Shortcuts](#keyboard-shortcuts)
- [Scripting](#scripting)
  - [Variables](#variables)
  - [Conditionals](#conditionals)
  - [Shifting Arguments](#shifting-arguments)
  - [Exit Codes](#exit-codes)
  - [Silence Output](#silence-output)

## Resources

[Linux Cheatsheet](linux.md)

[Bash Reference Manual](https://www.gnu.org/software/bash/manual/bash.html)

[Shell Script Best Practices](https://sharats.me/posts/shell-script-best-practices/)

## Keyboard Shortcuts

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

## Scripting

### Variables

- get variable: `$VARIABLE` or `${VARIABLE}`
- get variable or get default if null or not set: `${VARIABLE:-default}`
- get variable or assign default if null or not set: `${VARIABLE:=default}`

### Conditionals

- condition not true: `! conditional` or `! [ conditional ]`
- strings
  - length is zero: `-z`
  - length is non-zero: `-n`
  - equal: `s1 -eq s2` or `s1 = s2`
  - not equal: `s1 -ne s2` or `s1 != s2`
  - s1 < s2: `s1 -lt s2` or `s1 < s2`
  - s1 <= s1: `s1 -le s2`
  - s1 > s2: `s1 -gt s2` or `s1 > s2`
  - s1 >= s2: `s1 -ge s2`
- files
  - exists: `-a` or `-e`
  - directory: `-d`
  - regular file: `-f`
  - symbolic link: `-h` or `-L`
  - block special file: `-b`
  - character special file: `-c`
  - named pipe (FIFO): `-p`
  - socket: `-S`
  - readable: `-r`
  - writable: `-w`
  - executable: `-x`
  - size greater than zero: `-s`
  - modified since it was last read: `-N`
  - set-group-id bit set: `-g`
  - set-user-id bit is set: `-u`
  - "sticky" bit set: `-k`
  - owned by effective group id: `-G`
  - owned by effective user id: `-O`
  - f1 and f2 refer to the same device and inode numbers:  `f1 -ef f2`
  - f1 is newer (mod date) or f1 exists and f2 does not: `f1 -nt f2`
  - f2 is newer (mod date) or f2 exists and f1 does not: `f1 -ot f2`
- file descriptor
  - open and refers to a terminal: `-t`
- shell options
  - enabled: `-o`
- shell variables
  - set and assigned a value: `-v`
  - set and is name reference: `-R`

### Shifting Arguments

- remove first argument: `shift`
- remove first n arguments(s): `shift n`

### Exit Codes

- get last command's exit code: `$?`

### Silence Output

- silence stdout: `command 1> /dev/null` or `command > /dev/null`
- silence stderr: `command 2>&1`
- silence stdout and stderr: `command > /dev/null 2>&1` or `command &> /dev/null` (bash >= v4)
- send stderr to stdout: `command 2>&1`
