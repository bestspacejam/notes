
# Ручная установка Let's Encrypt SSL сертификата в Debian 8 (Jessie)

## Установка Certbot
```shell
sudo apt-get install certbot -t jessie-backports
```

Если не установлен [*Jessie Backports*](https://backports.debian.org/Instructions/):

```shell
cd /etc/apt/sources.list.d/
echo 'deb http://ftp.debian.org/debian jessie-backports main' >> backports.list
```

## Получение сертификата

Для того чтобы получить сертификат для нескольких доменов, ключ `-d` можно использовать несколько раз:

```shell
certbot certonly -d example.com -d www.example.com --manual --preferred-challenges dns
```

## Обновление сертификата

```shell
certbot certonly -d example.com -d www.example.com --manual --keep-until-expiring --agree-tos --manual-public-ip-logging-ok --preferred-challenges dns
# Перезагрузка сервера для подключения обновлённых файлов
apachectl graceful
```
Опция `--dry-run` позволяет проверить запрос без фактического обновления файлов сертификатов

Использование Certbot:
<https://certbot.eff.org/docs/using.html>

