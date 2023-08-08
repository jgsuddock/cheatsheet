# Docker

- [Dockerfile](#dockerfile)
- [Run](#run)
- [Execute](#execute)
- [Examples](#examples)
  - [MySQL](#mysql)

## Dockerfile

> In Progress

## Run

`docker run`
- `--name container_name`: What should the container be named once it is running (makes one up if not supplied)
- `--env ENV_NAME=ENV_VALUE`: Sets the environment variable ENV_NAME to ENV_VALUE in running container
- `--volume /path/on/local/pc:/path/within/container`: Maps local path to container's path
- `-it`: Run the container interactive
- `-d`: Run the container as a daemon process
- `--rm`: Remove container after it is stopped
- `--pull=always`: Ensure the latest image from the server is used
- `image_name:tag_name_or_latest`: Examples - "python:3" or "hub.garmin.com/python:3"

```bash
docker run
  --name container_name # What should the container be named once it is running (makes one up if not supplied)
  --env ENV_NAME=ENV_VALUE # Sets the environment variable ENV_NAME to ENV_VALUE in running container
  --volume /path/on/local/pc:/path/within/container # Maps local path to container's path
  -it # Run the container interactive
  -d # Run the container as a daemon process
  --rm # Remove container after it is stopped
  --pull=always # Ensure the latest image from the server is used
  image_name:tag_name_or_latest # python:3 or hub.garmin.com/python:3
```

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
