# Git

- [Cheatsheet](#cheatsheet)
- [Resources](#resources)
- [Reverting Commits](#reverting-commits)
- [Merge](#merge)
- [Diff](#diff)
- [Diagnostics](#diagnostics)
- [Tags](#tags)

## Cheatsheet

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
  - tree view: `git log --graph`
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

## Resources

Development Styles - [Trunk Based Development](https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development) | [Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

## Reverting Commits

```bash
# Undo Local Commits On Current Branch And Return To Origin's Set.
git checkout {branch_name}
git reset --hard origin/{branch_name}
```

If you commit to the wrong branch, to fix it, you can look at the branch you want it to be on, then cherry pick the commit to the current branch. Push that to the server. Then look at the previous branch. Revert the wrong commit and push to server

You can also push the commit to the other branch if there are no commits between the commit and where the branch starts. This would be done instead of cherry picking the commit to the correct location. (push will move everything between commit and branch, cherry pick will only move the single commit).

Think of push/pull as actions with the server and cherry pick/commit/etc as actions locally.

```bash
# Remove changes to a file
git checkout -- <file.txt>
```

## Merge

```bash
# Open merge conflict in mergetool
git mergetool

# Set another mergetool
git config merge.tool vimdiff
git config merge.tool bc4
```

- list branches merged into master
  - local only: `git branch --merged master`
  - remote only: `git branch -r --merged master`
  - local and remote: `git branch -a --merged master`
- list branches merged into HEAD (i.e. tip of current branch): `git branch --merged`
- list branches that have not been merged: `git branch --no-merged`

## Diff

```bash
# Compare current commit with previous commit
git diff ^HEAD HEAD

# Compare current commit with previous commit on single file
git diff ^HEAD HEAD file.txt

# Display only filenames that have changed since previous commit
git diff --name-only ^HEAD HEAD

# Display only filenames that have changed since a specific tag
git diff --name-only refs/tags/tag-name
```

## Diagnostics

```bash
# Output Remote Repo Address
git remote show origin
```

## Tags

```bash
# List Tags
git tag -l

# List Tags Matching Wildcard
git tag -l "v1.*"

# Add Local Tag
git tag tag-name

# Add Local Tag (Override If Already Exists)
git tag -f tag-name

# Push Local Tag To Remote
git push origin refs/tags/tag-name

# Pull Tags From Remote
git fetch --tags

# Pull Tags From Remote (Override Local Tags If Exist)
git fetch --tags -f

# Pull Specific Tag From Remote
git fetch origin refs/tags/tag-name:refs/tags/tag-name

# Pull Specific Tag From Remote (Override Local Tag If Exists)
git fetch origin +refs/tags/tag-name:refs/tags/tag-name

# Check If Tag Exists On Remote
git ls-remote origin refs/tags/tag-name

# Check If Tag Exists On Remote (Set Exit Code For CI/CD)
git ls-remote origin --exit-code origin refs/tags/tag-name
```
