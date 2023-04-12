# linux quick reference

- [troubleshooting](#troubleshooting)
- [directories](#directories)
- [bash](#bash)
- [tmux](#tmux)
- [vim](#vim)
- [git](#git)

# troubleshooting

[linux cheatsheet](linux.md)

- system info: `uname` or `uname -a`
- network
  - ip: `ifconfig` or `ip addr show`
  - dns: `dig google.com`
  - open ports: `netstat -tulpn`
  - test tcp: `nc -vz google.com 80,443`
  - status code: `curl -sS "https://localhost:8080/animals"`
  - download file: `curl -O "https://www.digitalocean.com/robots.txt"`
- storage
  - disk space: `df -ah` or `vgs` (disk space in volume)
  - directory size: `du -sh /var/logs`
  - directory size (breakout): `du -ah --max-depth=1 /var`
  - swap: `swapon --show size`
- services
  - status: `systemctl status nginx` (new) or `service nginx status` (old)
  - logging: `journalctl -u tomcat.service --since today`
  - cronjob edit: `crontab -e`
- processes: `htop` or `ps aux`
- files
  - search (files older than 60 min): `find . -mmin +60 -type f`
  - search and list: `find . -type f -exec ls -l {} +`
- symlinks
  - file: `ln -s /points/here.txt here.txt`
  - dir: `ln -sn /points/here here`
- mounts:
  - list: `mount`
  - add: `mount /dev/sda1`
  - boot mounts: `less /etc/fstab`
- permissions
  - owner: `chown username:group file.txt` or `chown -R username:group directory` (recurse)
  - read/write: `chmod 755 directory` (rwx > owner|group|others)
  - check: `ls -l file.txt`
- history
  - logins: `last` or `last -n 5`
  - reboots: `last reboot` or `last reboot -s today` (only today)
- manuals: `man netstat`

# directories

[linux cheatsheet](linux.md)

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

# bash

[bash cheatsheet](bash.md)

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

# tmux

[tmux cheatsheet](tmux.md)

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

[vim cheatsheet](vim.md)

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

# git

[git cheatsheet](../git/git.md)

- clone: `git clone ssh://source.com/repo`
- remotes
  - list current: `git remote -v`
- branches
  - list: `git branch` or `git branch -r` (remote)
  - checkout: `git checkout branch-name`
  - new: `git branch branch-name` or `git checkout -b branch-name`
  - delete: `git branch -d branch-name`
  - reset: `git reset --hard origin/branch-name`
- commits
  - reset: `git checkout -- file.txt`
- tags
  - list: `git tag -l` or `git tag -l "v1.*"`
  - pull: `git fetch --tags` or `git fetch --tags -f` (override local)
  - push: `git push origin refs/tags/tag-name`
- diff
  - repo: `git diff` or `git difftool`
  - current | commit: `git diff HEAD`
  - commit | prev commit: `git diff ^HEAD HEAD`
  - file: `git diff ^HEAD HEAD file.txt`
  - filename only: `git diff --name-only ^HEAD HEAD`
- merge
  - resolve merge: `git mergetool`
