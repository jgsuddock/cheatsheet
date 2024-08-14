# SSH Cheatsheet

- [Generating Keys](#generating-keys)
- [Authorized Keys](#authorized-keys)
- [Permissions](#permissions)

## Generating Keys

1. Backup the keys in ~/.ssh (id_rsa, id_rsa.pub, id_ed25519, id_ed25519.pub, etc)
2. Change directory to ~/.ssh
3. Generate new key: `ssh-keygen -t rsa -b 4096` or `ssh-keygen -t ed25519` or `ssh-keygen -t ed25519 -C "new_comment"`

## Authorized Keys

To use SSH keys to login to another box, you can use authorized keys.

1. Copy the public key (probably in ~/.ssh/id_rsa.pub) from the box you want to SSH from
2. Create a new file in your ssh directory called authorized_keys (~/.ssh/authorized_keys)
3. In that new file, paste the contents from the public key from the source box.
4. Test connection: `ssh USERNAME@HOSTNAME`
  a. If issues occur, you can try running `ssh -vvv USERNAME@HOSTNAME` to debug the issues

## Fix Known Hosts Keys

1. Get key for server: `ssh-keyscan -t rsa -p server_port server_ip`
2. Edit known hosts file and add new key: `vim ~/.ssh/known_hosts`

## Permissions

The permissions for your ssh directory should be as follows:

| Directory | Permission |
|---|---|
|~/.ssh|700|
|~/.ssh/id_rsa|600|
|~/.ssh/id_rsa.pub|644|
|~/.ssh/known_hosts|644|
|~/.ssh/authorized_keys|644|
