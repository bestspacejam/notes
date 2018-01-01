# Примеры использования Certbot

## Ручная генерация

### Подтверждение владения доменом через HTTP-запрос

```shell
certbot certonly \
	-n \
	--manual \
	--preferred-challenges http \
	-m admin@example.com \
	-d example.com
```

## Автоматическая генерация

### Подтверждение владения доменом с сохранением файла в директорию веб-сервера (`--webroot`)

```shell
certbot certonly \
	-n \
	--webroot \
	--dry-run \
	--agree-tos \
	--email admin@example.com \
	-w /usr/share/nginx/html \
	-d example.com
```

**Замечание:** Веб-сервер должен быть настроен на отдачу файлов из указанной директории.


## Генерация с помощью Docker контейнера


```shell
docker run \
	-ti \
	--rm \
	-p 80:80 \
	-p 443:443 \
	-v $(pwd)/letsencrypt:/etc/letsencrypt \
	certbot/certbot \
	certonly \
		--standalone
		--agree-tos \
		-m admin@example.com \
		-d example.com
```


Сертификат сохраняется в директории `/etc/letsencrypt/archive/<domain>` и доступен через символическую ссылку из директории `/etc/letsencrypt/live/<domain>/cert.pem`)
См. подробнее: [Where are my certificates?](https://certbot.eff.org/docs/using.html#where-are-my-certificates)


## Проверка генерации сертификата

Можно использовать флаг `--test-cert` или `--dry-run` для проверки, без генерации файла сертификата.
