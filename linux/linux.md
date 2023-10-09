# Linux

- [Cheatsheet](#cheatsheet)
- [Resources](#resources)
- [Manuals](#manuals)
- [Navigation](#navigation)
- [Permissions](#permissions)
  - [File/Directory Ownership](#filedirectory-ownership)
  - [File/Directory Read/Write/Execute Permissions](#filedirectory-readwriteexecute-permissions)
  - [SSH Key Permissions](#ssh-key-permissions)
- [String Manipulation](#string-manipulation)
  - [grep](#grep)
  - [sed](#sed)
  - [awk](#awk)
- [Storage](#storage)
  - [Disk / Drive](#disk--drive)
  - [Directory / File](#directory--file)
  - [Swap](#swap)
- [Processes](#processes)
  - [top / htop](#top--htop)
  - [Init System](#init-system)
  - [Cron Jobs](#cron-jobs)
- [Network](#network)
  - [curl](#curl)
  - [ssh](#ssh)
  - [nc](#nc)
  - [nmap](#nmap)
  - [netstat](#netstat)
- [Directories](#directories)

## Cheatsheet

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
  - open files: `lsof +L1` (won't show full size in du)
- memory
  - usage: `free -m` or `free -h` (human readable)
  - usage (top 10): `ps aux --sort=-%mem | head`
- cpu
  - config: `lscpu`
- services
  - status: `systemctl status nginx` (new) or `service nginx status` (old)
  - logging: `journalctl -u tomcat.service --since today` or `journalctl _PID=1234`
  - cronjob edit: `crontab -e`
- processes:
  - manager: `htop` or `top`
  - list: `ps aux`
  - used ports: `netstat -lpn` or `netstat -tulpn` (tcp/udp only)
  - listening tcp ports: `lsof -nP -iTCP -sTCP:LISTEN`
- search
  - file names: `find . -name *.jpg`
  - files older than 60 min: `find . -mmin +60 -type f`
  - list matching file names: `find . -type f -exec ls -l {} +`
  - files containing keyword: `grep -Rnw '/path/to/dir' -e 'TEXT_TO_FIND'`
  - files containing keyword: `grep --include=\*.{c,h} -Rnw '/path/to/dir' -e 'TEXT_TO_FIND'`
  - files containing keyword: `find . -type f -name "*.xml" | xargs egrep -i 'TEXT_TO_FIND'`
- symlinks
  - file: `ln -s /points/here.txt from-here.txt` or `-sf` (force)
  - dir: `ln -sn /points/here from-here` or `-snf` (force)
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
  - uptime: `uptime`
- gzip
  - compress: `tar -czvf archive.tar.gz /path/to/directory-or-file`
  - extract: `tar -xvf archive.tar.gz -C /path/to/new-directory-or-file`
- manuals: `man netstat`

## Resources

- [Bash Cheatsheet](bash.md)

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
# Lookup up ownership of directory/file
ls -l path/to/directory_or_file

# Change ownership of directory to certain user and group
sudo chown username:group directory

# Change ownership of directory and all child files to certain user and group
sudo chown -R username:group directory
```

### File/Directory Read/Write/Execute Permissions

Reading/Changing Permissions:

```bash
# Lookup up ownership of directory/file
ls -l path/to/directory_or_file

# Change permissions of directory to (drwxrwxrwx)
sudo chmod 777 directory

# Change permissions of directory to (drwxr-xr-x)
sudo chmod 755 directory
```

Permission Notation (`drwxrwxrwx`):

| d | rwx | rwx | rwx |
| --- | --- | --- | --- |
| File Type | User/Owner | Group | Others |

File Types:

| Key | Type |
| --- | --- |
| `d` | Directory |
| `l` | Symlink |
| `-` | File |

Read/Write/Execute Permissions For Each Group - Octal Conversions:

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

### SSH Key Permissions

```bash
# Directory permissions (drwx------)
sudo chmod 700 ~/.ssh
# Public key (-rw-r--r--)
sudo chmod 644 ~/.ssh/id_rsa.pub
# Private key (-rw-------)
sudo chmod 600 ~/.ssh/id_rsa
```

## String Manipulation

### grep

```bash
# Grep - searches for where substring exists in string. For outputs of multiple lines, each line will be checked individually
grep "substring"

# This will return the first row in a list of rows.
head -1

# Find file recursively in directory that contains a certain string
find /path/to/dir -type f -name "*.xml" | xargs egrep -i 'TEXT_TO_FIND'
grep -Rnw '/path/to/dir/' -e 'TEXT_TO_FIND'
grep --include=\*.{c,h} -Rnw '/path/to/dir/' -e "TEXT_TO_FIND"
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
  
# 10 largest directories within dir_name (recursive)
du -a /src/dir_name | sort -n -r | head -n 10

# Show file sizes at current level
du -cha --max-depth=1 /var | grep -E "M|G"
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
# Find the tomcat process running
ps -ef | grep tomcat
```

### top / htop

top and htop are process managerers for linux. `htop` is a newer version and easier to use. `top` typically comes preinstalled on most systems.

```bash
htop
```

```bash
top
```

Add/Rearrange/Sort Fields:

1. Press `F` to display field listing
2. Press `Up Arrow` or `Down Arrow` to move cursor.
3. Press `Space` to enable/disable field (enabled fields are proceeded by an astrisk `*`).
4. Press `Right Arrow` and then use arrow keys to rearrange field. Press `Left Arrow` to keep selection.
5. Press `S` to sort by that desired field.
6. Press `Q` to exit back to top view.

Sort By Memory:

1. Press `Shift + M` or use the argument `top -o %MEM`

Thread View:

1. Press `T` to view thread view

### Init System

#### SystemD

Most distributions are moving towards this

[Documentation](https://access.redhat.com/articles/754933)

[Fedora Documentation](https://fedoraproject.org/wiki/Systemd#systemd_documentation)

[RHEL Documentation](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/chap-Managing_Services_with_systemd.html)

```bash
# List all services
sudo systemctl --all list-unit-files --type=service

# List all services (directory)
ls /lib/systemd/system/*.service /etc/systemd/system/*.service

# View tomcat service config
vim /etc/systemd/system/tomcat.service

# Start service
sudo systemctl start tomcat.service
```

Enabling/Disabling
```bash
# Enable/Disable service
sudo systemctl enable tomcat.service

# Check if service enabled
sudo systemctl is-enabled tomcat.service
```

`systemctl enable` works by manipulating symlinks in `/etc/systemd/system/` (for system daemons). When you `enable` a service, it looks at the `WantedBy` lines in the `[Install]` section, and plops symlinks in those `.wants` directories.

`systemctl disable` does the opposite.

Logging
```bash
# View All Logs
sudo journalctl

# Today Only
sudo journalctl --since today

# sshd Daemon Logs
sudo journalctl -u sshd

# service logs
sudo journalctl -u tomcat.service
```

#### System V

Older distributions use this

[Documentation](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Installation_Guide/s1-boot-init-shutdown-sysv.html)

```bash
# List all services
sudo service --status-all

# List all init scripts
ls /etc/init.d/

# List all run-level symlinks
ls /etc/rc*.d/

# View tomcat service config
vim /etc/inti.d/tomcat
```

#### Upstart

Older debian instances use this

[Documentation](http://upstart.ubuntu.com/cookbook/)

```bash
# List all services
sudo initctl list

# List all services and their config
sudo initctl list | awk '{ print $1 }' | xargs -n1 initctl show-config
```

## Cron Jobs

```bash
cat /var/spool/cron/root
```

## Network

```bash
# Show address mapping on server
lp addr show

# DNS Lookup Tool
dig google.com
```

### curl

```bash
# Curl - Returns response from endpoint
curl -sS "http://localhost:8000/animals")

# Curl - Download file (keeping name)
curl -O "https://www.digitalocean.com/robots.txt"
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

### nc
```bash
# Test TCP Connection On Port 80 & 443
nc -vz google.com 80,443
```

### nmap

```bash
todo
```

### netstat

```bash
# Check if a certain port is open (may need sudo)
netstat -lnp | grep 8080
```

## Cron

From [https://www.baeldung.com/cron-expressions](https://www.baeldung.com/cron-expressions) and [https://docs.oracle.com/cd/E12058_01/doc/doc.1014/e12030/cron_expressions.htm](https://docs.oracle.com/cd/E12058_01/doc/doc.1014/e12030/cron_expressions.htm)

### Cron Tab

Cron schedule stored in `/var/spool/cron/crontabs`. However, to edit, use the crontab command

```bash
crontab -e
```

### Cron Expression

```
<minute> <hour> <day-of-month> <month> <day-of-week> <command>
```

| Name | Required | Allowed Values | Allowed Special Characters
|---|---|---|---|
| Minutes | Y | 0-59 | `, - * /` |
| Hours | Y | 0-23 | `, - * /` |
| Day of month | Y | 1-31 | `, - * ? / L W C` |
| Month | Y | 0-11 or JAN-DEC |  `, - * /` |
| Day of week | Y | 1-7 or SUN-SAT | `, - * ? / L C #` |
| Command | path | --- |

Special Characters
- `*` - All
- `?` - Any
- `-` - Range (i.e. 10-11 in hour = 10th and 11th hour)
- `,` - Values (i.e. MON, WED, FRI)
- `/` - Increments (i.e. 5/15 in minute = 5, 20, 35, 50 minute of an hour)
- `L` - Last (i.e. L-3 = third to last day of calendar month)
- `W` - Weekday
- `#` - N-th Occurrence ( 6#3 in month = third friday of the month)

```
Expression                   Means
0 12 * * ?	             Fire at 12:00 PM (noon) every day
15 10 ? * *	             Fire at 10:15 AM every day
15 10 * * ?	             Fire at 10:15 AM every day
15 10 * * ? *	             Fire at 10:15 AM every day
* 14 * * ?	             Fire every minute starting at 2:00 PM and ending at 2:59 PM, every day
0/5 14 * * ?	             Fire every 5 minutes starting at 2:00 PM and ending at 2:55 PM, every day
0/5 14,18 * * ?	             Fire every 5 minutes starting at 2:00 PM and ending at 2:55 PM, AND fire every 5 minutes starting at 6:00 PM and ending at 6:55 PM, every day
0-5 14 * * ?	             Fire every minute starting at 2:00 PM and ending at 2:05 PM, every day
10,44 14 ? 3 WED	     Fire at 2:10 PM and at 2:44 PM every Wednesday in the month of March
15 10 ? * MON-FRI	     Fire at 10:15 AM every Monday, Tuesday, Wednesday, Thursday and Friday
15 10 15 * ?	             Fire at 10:15 AM on the 15th day of every month
15 10 L * ?	             Fire at 10:15 AM on the last day of every month
15 10 ? * 6L	             Fire at 10:15 AM on the last Friday of every month
15 10 ? * 6#3	             Fire at 10:15 AM on the third Friday of every month
0 12 1/5 * ?	             Fire at 12 PM (noon) every 5 days every month, starting on the first day of the month
11 11 11 11 ?	             Fire every November 11 at 11:11 AM
```

## Directories

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
