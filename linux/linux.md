# linux cheatsheet

- [directories](#directories)
- [troubleshooting](#troubleshooting)
- [bash](#bash)
- [tmux](#tmux)
- [vim](#vim)
- [git](#git)

# directories

- `/bin` - essential system binaries
- `/sbin` - essential system admin binaries
- `/boot` - files for booting system
- `/cdrom` - historical device mount location
- `/media` - system mounted devices
- `/mnt` - user mounted devices
- `/dev` - device files (includes partitions like `/dev/sda`)
    - `/dev/random` - produce random number
    - `/dev/null` - pipe output to here to discard
- `/etc` - system configuration files
- `/home` - each user’s home directories (protected to that user)
- `/lib` - essential shared libraries
- `/opt` - optional system packages
- `/proc` - kernel and process files
- `/root` - root user’s home directory
- `/run` - application transient file storage (sockets, process IDs, etc)
- `/srv` - website files or other system served data
- `/tmp` - temporary files
- `/usr` - user binaries and read only data
    - `/usr/bin` non-essential binaries
    - `/usr/sbin` non-essential admin binaries
    - `/usr/lib` - non-essential shared libraries
    - `/usr/local` - locally compiled applications
    - `/usr/share` - architecture-independent files
- `/var` - variable sized data (log files, databases, etc)

# troubleshooting

- system info: `uname` or `uname -a`
- network: `ifconfig` or `ip addr show`
- disk space: `df -ah`
- directory size: `du -sh /var/logs`
- services: `systemctl status nginx` (new) or `service nginx status` (old)
- processes: `htop` or `ps aux`
- open ports: `sudo netstat -tulpn`
- mounts:
    - list: `mount`
    - add: `mount /dev/sda1`
    - boot mounts: `less /etc/fstab`
- manuals: `man netstat`

# bash

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
    - cut to start of word: `Alt + W` or `Ctrl + W`
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

# tmux

- sessions
    - new: `tmux` or `tmux new -s newname`
    - attach: `tmux a` or `tmux a -t newname`
    - de-attach: `<Ctrl + B>` `D`
    - kill: `tmux kill-session -t newname`
    - list: `tmux ls`
- windows (include bind `Ctrl + B`)
    - new: `C`
    - next: `N`
    - previous: `P`
    - list: `W`
    - find: `F`
    - name: `,`
    - kill: `&`
- panes (include bind `Ctrl + B`)
    - new (vertical): `%`
    - new (horizontal): `"`
    - swap: `O`
    - kill: `X`
    - break into window: `+`
    - restore from window: `-`
    - toggle layout: `space`
    - show pane numbers: `Q`
    - move left: `{`
    - move right: `}`
    - zoom: `Z`
- edit
    - enter: `Ctrl + B` `[`
    - exit: `Q`
    - move: `arrow keys`
    - select
        - start: `Ctrl + S`
        - copy: `Alt + W`
        - clear: `Ctrl + G`

# vim

- open read-only: `vim -R file.txt` or `view file.txt`
- panes:
    - split horizontally: `:split`
    - split vertically: `:vsplit`
    - switch panes: `Ctrl + W`
- command mode
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
- insert mode
- visual mode
- .vimrc

```
set tabstop=2 shiftwidth=2 expandtab smarttab autoindent number mouse=n list listchars=lead:·,trail:·,tab:»␣
hi SpecialKey ctermfg=DarkGray
```

# git

- clone: `git clone ssh://source.com/repo`
- branch
    - new: `git branch BRANCH_NAME` or `git checkout -b BRANCH_NAME`
    - checkout: `git checkout BRANCH_NAME`
- diff
    - compare current with commit: `git diff HEAD`
    - compare commit with previous commit: `git diff ^HEAD HEAD` or `git diff ^HEAD HEAD file.txt` or `git diff --name-only ^HEAD HEAD`
