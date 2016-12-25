
Установка Letsencrypt SSL-сертификата в Debian 8 (jessie)

```bash
apt-get install python-certbot-apache -t jessie-backports
```

Для доменов 

```bash
certbot certonly -n -d example.com -d www.example.com
```

```bash
certbot -d example.com -d www.example.com --manual --preferred-challenges dns certonly
```

```
cd /etc/apt/sources.list.d/
echo 'deb http://ftp.debian.org/debian jessie-backports main' >> backports.list
```

Использование Certbot:
<https://certbot.eff.org/docs/using.html>

