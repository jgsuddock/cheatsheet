# Apache

- [References](#references)
- [Naming](#naming)
- [Config](#config)
- [Service](#service)

## References

- [Tomcat Cheatsheet](tomcat.md)

## Naming

In Debian systems, it is called apache2.

In RedHat systems, it is called httpd.

## Config

Default config path: `/etc/httpd/conf/httpd.conf`

Default public path: `/var/www/html`

## Service

Reload apache config: `sudo /etc/init.d/apache2 reload` or `sudo service httpd restart` or `sudo httpd -k restart` 

Test apache config: `sudo httpd -t` -> looking for "Syntax OK"
