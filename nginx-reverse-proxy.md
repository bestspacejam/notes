# Проксирование в NGINX

```
lacation /static/ {
	proxy_pass http://127.0.0.1;
}
```

## Директива [proxy_pass](https://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_pass)

```
proxy_pass http://127.0.0.1/public/;
# GET /static/assets/style.css -> http://127.0.0.1/public/assets/style.css
```

Удаляет часть /static/ из оригинального запроса и добавляет оставшееся в конец проксируемого URI

```
proxy_pass http://127.0.0.1;
# GET /static/assets/style.css -> http://127.0.0.1/static/assets/style.css
```

Добавляет весь оргигинальный запрос в конец проксируемого URI.
В случае изменения оригинального запроса с помощью регулярных выражений передаётся изменёный запрос.

```
proxy_pass http://127.0.0.1/public$request_uri;
# GET /static/assets/style.css -> http://127.0.0.1/public/static/assets/style.css
```
Добавляет весь оргигинальный запрос в конец проксируемого URI  


