# Salt

## Commands

### Apply Highstate

```bash
# Apply highstate from master
salt '*' state.highstate

# Apply highstate from minion
salt-call state.highstate
```

### Enable/Disable Highstate

```bash
# Disable the ability for the name* box to pull new state changes. This disables both the box pulling with salt-call as well as the master pushing.
salt 'name*' state.disable highstate

# Re-enable the ability for the name* box to pull new state changes.
salt  'name*' state.enable highstate

# List all currently disabled boxes
salt '*' state.list_disabled
```

### Execute Commands On Minions

```bash
salt '*' cmd.run 'ls -l /etc'
```

## Minion Keys

```bash
# List all minions
salt-key -L
```

## Linting

```bash
# Lint the top.sls (no results == good)
salt-lint top.sls
```

## Grains

https://docs.saltproject.io/en/latest/topics/grains/index.html

```bash
# Listing Available Grains
salt '*' grains.ls

# Listing Grains Data
salt '*' grains.items
```
