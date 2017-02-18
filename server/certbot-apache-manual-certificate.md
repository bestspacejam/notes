
#Установка Let's Encrypt SSL сертификата в Debian 8

```shell
apt-get install python-certbot-apache -t jessie-backports
```

Для нескольких доменов (с *www* и *без www*):

```shell
certbot certonly -n -d example.com -d www.example.com
```

```shell
certbot -d example.com -d www.example.com --manual --preferred-challenges dns certonly
```

```shell
cd /etc/apt/sources.list.d/
echo 'deb http://ftp.debian.org/debian jessie-backports main' >> backports.list
```

Использование Certbot:
<https://certbot.eff.org/docs/using.html>

