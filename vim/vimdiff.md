# Vim Diff

## Cheatsheet

- navigate
  - next diff: `]c`
  - previous diff: `[c`
- apply diff:
  - other to current: `:diffget` or `diff obtain` or `do`
  - current to other: `:diffput` or `diff put` or `dp`
- folded text
  - open: `zo`
  - close: `zc`
- windows
  - next window: `Ctrl+W Ctrl+W`
  - windows info: `:ls`
- quit all buffers: `qall!`  
- Re-scan the file for differences: `:diffupdate`
- Get a diff of files on buffers: `:diffthis`
- Return to normal mode: `:diffoff`
- change color scheme: `:colorscheme murphy` or `:colorscheme ` + `Tab` to see options

## Windows

- **Upper-Left** - The local/target branch
- **Upper-Center** - The most common ancestor of the 'target' and the 'merge' branch
- **Upper-Right** - The remote/merge branch
- **Bottom** - The product of this merge operation
