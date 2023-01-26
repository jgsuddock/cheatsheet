# Bash

# Resources

[Bash Reference Manual](https://www.gnu.org/software/bash/manual/bash.html)

[Shell Script Best Practices](https://sharats.me/posts/shell-script-best-practices/)

# General

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

# Find file recursively in directory that contains a certain string
find /path/to/dir -type f -name "*.xml" | xargs egrep -i 'TEXT_TO_FIND'

# Print XML File By Cleaning Up And Sorting Tags
cat /path/to/file.xml | sed -re 's/>/>\n/g' | sort -u | less

# SED - Streamline Editor (https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/)

# replace the first instance of "unix" in every line with "linux"
sed 's/unix/linux' inputfile.txt

# replace the first two instance of "unix" in every line with "linux"
sed 's/unix/linux/2' inputfile.txt

# replace the all instances of "unix" with "linux"
sed 's/unix/linux/g' inputfile.txt

# replace every third instance of "unix" with "linux"
sed 's/unix/linux/3g' inputfile.txt

# Parse JSON
'[{"name": "a", "value": "a1"}, {"name": "b", "value": "b2"}]' | jq -r '.[].name'
# Prints: "a\nb"

# Helm get all release names and then delete each of those helm releases
for i in $(helm ls -a -o json | jq -r '.[].name'); do helm delete $i; done
```

## String Manipulation

```bash
# Grep - searches for where substring exists in string. For outputs of multiple lines, each line will be checked individually
grep "substring"

# This will return the first row in a list of rows.
head -1

# AWK - need to look into this more
echo "first    second    third" | awk '{print $3}'
#     this returns `third`
```

## Processes

```bash
# Process Manager
htop

# Disk Space
#     Drive Space (Human Readable)
df -H
df -H /dev/sda1

#    Directory Space
du -h /src/dir_name # List size of all child directories of dir_name (recursive)
du -sh /src/dir_name # List size of dir_name only
du -a /src/dir_name | sort -n -r | head -n 10 # 10 largest directories within dir_name (recursive)

# Find the tomcat process running
ps -ef | grep tomcat
```

## Editing

```bash
# Vim - Read-Only
vim -R filename.txt
```

# Network

## Curl

```bash
# Curl - Returns response from endpoint
curl -sS "http://localhost:8000/animals")

# Show address mapping on server
lp addr show

# DNS Lookup Tool
dig google.com

# Test TCP Connection On Port 80 & 443
nc -vz google.com 80,443

# Check if a certain port is open (may need sudo)
netstat -lnp | grep 8080
```

## SSH

```bash
# Connect to SSH Client
ssh username@computername.domain.com

# Execute Command on SSH Client
ssh username@computername.domain.com 'ls -al ~'

# Execute Command on Multiple SSH Clients
parallel-ssh -i -H 'computername1 computername 2' ls -al ~
```

# Keyboard Shortcuts

| Action | Keyboard Shortcut |
| --- | --- |
| Move cursor to start of line | Ctrl + A |
| Move cursor to end of line | Ctrl + E |
| Move back one character | Ctrl + B |
| Move back one word | Alt + B |
| Move forward one character | Ctrl + F |
| Move forward one word | Alt + F |
| Toggle between first and current position | Ctrl + XX |
| Delete current character | Ctrl + D |
| Cut the last word | Ctrl + W |
| Cut word before the cursor | Alt + W |
| Cut word after the cursor | Alt + D |
| Cut everything before the cursor | Ctrl + U |
| Cut everything after the cursor | Ctrl + K |
| Clean up the line | Ctrl + E Ctrl + U |
| Cancel the command | Ctrl + C |
| Paste the last deleted command | Ctrl + Y |
| Undo | Ctrl + _ |
| Save Current Line As Comment | Alt + Shift + # |
| Clear the terminal | Ctrl + L |
| Search command in history - type the search term | Ctrl + R |
| End the search at current history entry | Ctrl + J |
| Cancel the search and restore original line | Ctrl + G |
| Next command from the History | Ctrl + N |
| Previous command from the History | Ctrl + P |
| Stop Searching History (Return to Blank Line) | Ctrl + Alt + > |
- Recall the deleted command: Ctrl+Y (then Alt+Y)
- Remove the forward words for example, if you are middle of the command: Ctrl+K
- Remove characters on the left, until the beginning of the word: Ctrl+W