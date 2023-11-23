# Certbot
## Шпаргалка по командам
```shell
# Списиок сертификатов
certbot certificates

# Удаление сертификата
certbot delete --cert-name domain-name.ru
```
## Ручная генерация сертификата

Подтверждение владения доменом через HTTP-запрос:

```shell
certbot certonly \
  -n \
  --manual \
  --preferred-challenges http \
  --email admin@example.com \
  --domains example.com
```
## Автоматическое получение сертификата 

```shell
certbot certonly \
  -n \
  --agree-tos \
  --webroot \
  --webroot-path /var/www/html \
  --email admin@example.com \
  --domains example.com
```

Подтверждение владения доменом с сохранением файла в директорию `/.well-known/acme-challenge` веб-сервера.
**Замечание:** Веб-сервер должен быть настроен на отдачу файлов из директории указанной в параметре `--webroot-path` .

Для Nginx можно подключить вот такую "ловушку":

```nginx
location /.well-known/acme-challenge/ {
  root /var/www/html;
}
```

Сертификат сохраняется в директории `/etc/letsencrypt/archive/<domain>` и доступен через символическую ссылку из директории `/etc/letsencrypt/live/<domain>/cert.pem`)
См. подробнее: [Where are my certificates?](https://certbot.eff.org/docs/using.html#where-are-my-certificates)

## Проверка генерации сертификата

Можно использовать флаг `--test-cert` или `--dry-run` для проверки, без генерации файла сертификата.

## Генерация с помощью Docker контейнера

```shell
docker run \
  -ti \
  --rm \
  -p 80:80 \
  -p 443:443 \
  -v "$PWD"/letsencrypt:/etc/letsencrypt \
  certbot/certbot \
  certonly \
    --standalone
    --agree-tos \
    -m admin@example.com \
    -d example.com
```

