# linux quick reference

- [troubleshooting](linux.md#troubleshooting)
- [directories](linux.md#directories)
- [bash](bash.md#commands)
- [tmux](#tmux)
- [vim](#vim)
- [git](#git)

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
