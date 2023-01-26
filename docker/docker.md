# Docker

# MySQL

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

# Commands