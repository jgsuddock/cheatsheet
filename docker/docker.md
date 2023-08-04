# Docker

- [Dockerfile](#dockerfile)
- [Run](#run)
- [Execute](#execute)
- [Examples](#examples)
  - [MySQL](#mysql)

## Dockerfile

> In Progress

## Run

```bash
# Pull python3 container, exec into it, then remove container once exited
docker run -it --rm --pull=always python3:latest

# environment variables
docker run -it --env ENVNAME=bob python3:latest

# Volume Mounts
docker run -it --mount type=bind,source=C:\git\dir_name,target=/mnt/dir_name python3:latest #verbose
docker run -it -v C:\git\dir_name=/mnt/dir_name python3:latest
```

## Execute

```bash
# Exec into container
docker exec -it container-name bash

# Exec into container as root user
docker exec -it -u 0 container-name bash
```

## Examples

### MySQL

```bash
docker run --name mysql -d \
-e MYSQL_ROOT_PASSWORD=password \
-v mysql:/var/lib/mysql \
--restart unless-stopped \
mysql:8
```

```bash
mkdir secrets
echo "P@$$w0rd" > secrets/mysql-root-password

docker run --name mysql -d \
-p 3306:3306 \
-e MYSQL_ROOT_PASSWORD_FILE=/run/secrets/mysql-root-password \
-v ./secrets:/run/secrets \
--restart unless-stopped \
mysql:8
```
