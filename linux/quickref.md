# linux quick reference

- [troubleshooting](linux.md#troubleshooting)
- [directories](linux.md#directories)
- [bash](bash.md#commands)
- [tmux](tmux.md#tmux)
- [vim](vim.md#vim)
- [git](#git)

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
