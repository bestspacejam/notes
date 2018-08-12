# Проксирование в NGINX

```
location /static/ {
	proxy_pass http://127.0.0.1;
}
```

Можно так же указать имя хоста:
```
location /static/ {
	proxy_pass http://frontend;
}
```
Надо учитывать, что Nginx при старте пытается резолвить все `upstream`, и если какой-то из них не отвечает - прокси сервер не стартует.

Для игнорирования разрешения имени при старте прокси-сервера можно использовать формат:

```
location /frontend/ {
  proxy_pass http://frontend$request_uri;
}
```

## Директива [proxy_pass](https://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_pass)

```
proxy_pass http://127.0.0.1/public/;
```

Удаляет часть /static/ из оригинального запроса и добавляет оставшееся в конец проксируемого URI

`/static/assets/style.css` -> `http://127.0.0.1/public/assets/style.css`


```
proxy_pass http://127.0.0.1;
```

Добавляет весь оргигинальный запрос в конец проксируемого URI.  
В случае изменения оригинального запроса с помощью регулярных выражений передаётся изменёный запрос.  
`/static/assets/style.css` -> `http://127.0.0.1/static/assets/style.css`

```
proxy_pass http://127.0.0.1/public$request_uri;
```

Добавляет весь оргигинальный запрос в конец проксируемого URI

`/static/assets/style.css` -> `http://127.0.0.1/public/static/assets/style.css`


## Разрешение DNS имён при запуске внутри Docker-контейнера 

Docker использует для сервера имён адрес `127.0.0.11` 
```
location /frontend/ {
  resolver 127.0.0.11 valid=60s;
  proxy_pass http://frontend;
}
```
