# Bash

- [Resources](#resources)
- [Manuals](#manuals)
- [Navigation](#navigation)
- [Permissions](#permissions)
  - [File/Directory Ownership](#filedirectory-ownership)
  - [File/Directory Read/Write/Execute Permissions](#filedirectory-readwriteexecute-permissions)
- [String Manipulation](#string-manipulation)
  - [grep](#grep)
  - [sed](#sed)
  - [awk](#awk)
- [Storage](#storage)
  - [Disk / Drive](#disk--drive)
  - [Directory / File](#directory--file)
  - [Swap](#swap)
- [Processes](#processes)
  - [Cron Jobs](#cron-jobs)
- [Scripting](#scripting)
- [Network](#network)
  - [curl](#curl)
  - [ssh](#ssh)
- [Keyboard Shortcuts](#keyboard-shortcuts)

## Resources

[Bash Reference Manual](https://www.gnu.org/software/bash/manual/bash.html)

[Shell Script Best Practices](https://sharats.me/posts/shell-script-best-practices/)

## Manuals

```bash
# Open the manual for tmux
man tmux
```

Once open, type `/SearchTerm` to search for text. Use `N` to go to next result and `P` to go to the previous result.

## Navigation

```bash
# List children in directory
ls
ls -l # long form output
ls -a # include hidden files
ll # alias for `ls -l`

# Set Alias in Bash (can be set in ~/.bashrc to apply to profile)
alias ll='ls -l'

# eval -> command substitution
val=$($1)
eval res='${val}'

# Find file recursively in directory that contains a certain string
find /path/to/dir -type f -name "*.xml" | xargs egrep -i 'TEXT_TO_FIND'

# Print XML File By Cleaning Up And Sorting Tags
cat /path/to/file.xml | sed -re 's/>/>\n/g' | sort -u | less

# Parse JSON
'[{"name": "a", "value": "a1"}, {"name": "b", "value": "b2"}]' | jq -r '.[].name'
# Prints: "a\nb"

# Helm get all release names and then delete each of those helm releases
for i in $(helm ls -a -o json | jq -r '.[].name'); do helm delete $i; done
```

## Permissions

### File/Directory Ownership

```bash
# Change ownership of directory to certain user and group
sudo chown username:group directory

# Change ownership of directory and all child files to certain user and group
sudo chown -R username:group directory
```

### File/Directory Read/Write/Execute Permissions

```bash
# Change permissions of directory to (drwxrwxrwx)
sudo chmod 777 directory

# Change permissions of directory to (drwxr-xr-x)
sudo chmod 755 directory
```

### SSH Key Permissions

```bash
# Directory permissions (drwx------)
sudo chmod 700 ~/.ssh
# Public key (-rw-r--r--)
sudo chmod 644 ~/.ssh/id_rsa.pub
# Private key (-rw-------)
sudo chmod 600 ~/.ssh/id_rsa
```

- drwxrwxrwx:
    - `d` - File Type (`d` = directory, `l` = symlink, `-` = file)
    - `rwx` - User (Owner)
    - `rwx` - Group
    - `rwx` - Others

Read/Write/Execute Permissions For Each Group - Octal Conversions

| Octal | String Representation | Permissions |
| --- | --- | --- |
| 0 | - - - | No permissions |
| 1 | - - x | Only execute |
| 2 | - w - | Only write |
| 3 | - w x | Write and Execute |
| 4 | r - - | Only Read |
| 5 | r - x | Read and Execute |
| 6 | r w - | Read and Write |
| 7 | r w x | Read, Write, and Execute |

## String Manipulation

### grep

```bash
# Grep - searches for where substring exists in string. For outputs of multiple lines, each line will be checked individually
grep "substring"

# This will return the first row in a list of rows.
head -1
```

### sed

Streamline Editor ([sed command in linux unix with examples](https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/))

```bash
# replace the first instance of "unix" in every line with "linux"
sed 's/unix/linux' inputfile.txt
 
# replace the first two instance of "unix" in every line with "linux"
sed 's/unix/linux/2' inputfile.txt
 
# replace the all instances of "unix" with "linux"
sed 's/unix/linux/g' inputfile.txt
 
# replace every third instance of "unix" with "linux"
sed 's/unix/linux/3g' inputfile.txt
```

### awk

```bash
echo "first    second    third" | awk '{print $3}'
    # returns `third`

# Search directory for file with SEARCH_STRING and get the path of it
ls -l /path/to/dir | grep SEARCH_STRING | awk '{print $9}'
```

## Storage

### Disk / Drive

```bash
# Disk/Drive Space
df -H # Human readable format
df -H /dev/sda1 # Display only `/dev/sda1` drive space
```

### Directory / File

```bash
# Directory Space
du /src/dir_name
  -h # Human readable format
  -s # Current directories overall size (i.e. size of `/src/dir_name`)
  -a # Recursive search (all files and directories below)
  --time # Include modification date in the results
du -a /src/dir_name | sort -n -r | head -n 10 # 10 largest directories within dir_name (recursive)
```

### Swap

```bash
# Get Available Swap Space
sudo swapon --show size

# Get Available Disc Space in Volume Group
sudo vgs

# Extend Swap Space to 2G
sudo swapoff -a
sudo lvextend -L2G /dev/osvg/swap_lv
sudo mkswap -f /dev/osvg/swap_lv
sudo swapon -a
```

## Processes

```bash
# Process Manager
htop

# Find the tomcat process running
ps -ef | grep tomcat
```

## Cron Jobs

```bash
cat /var/spool/cron/root
```

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

## Network

### curl

```bash
# Curl - Returns response from endpoint
curl -sS "http://localhost:8000/animals")

# Curl - Download file (keeping name)
curl -O "https://www.digitalocean.com/robots.txt"

# Show address mapping on server
lp addr show

# DNS Lookup Tool
dig google.com

# Test TCP Connection On Port 80 & 443
nc -vz google.com 80,443

# Check if a certain port is open (may need sudo)
netstat -lnp | grep 8080
```

### ssh

```bash
# Connect to SSH Client
ssh username@computername.domain.com

# Execute Command on SSH Client
ssh username@computername.domain.com 'ls -al ~'

# Execute Command on Multiple SSH Clients
parallel-ssh -i -H 'computername1 computername 2' ls -al ~
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
