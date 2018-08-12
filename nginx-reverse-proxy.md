# Проксирование в NGINX

```
location /static/ {
	proxy_pass http://127.0.0.1;
}
```

Вместо IP-адреса можно указать имя хоста:

```
location /static/ {
	proxy_pass http://frontend;
}
```

**Важно:** Nginx при старте пытается резолвить все хосты `upstream`, и если какой-то из них не отвечает, то прокси-сервер не запускается.


### Игнорирование разрешения имени при старте:

```
location /frontend/ {
  proxy_pass http://frontend$request_uri;
}
```
Тогда `upstream` будет резолвится при каждом обращении.

Для включения динамического рарешения имён можно указать имя хоста через переменную. При указании переменной Nginx сначала будет искать  значение в группе серверов, а затем если не найдёт будет динамически резолвить его как имя хоста, через сервер указанный в директиве `resolver` или в файле `/etc/resolv.conf`.

```
location /frontend/ {
  set $upstream_host "frontend";
  proxy_pass http://$upstream_host;
}
```
Дополнительно почитать можно тут:
- [Nginx proxy_pass DNS Cache](https://www.nadeau.tv/nginx-proxy_pass-dns-cache/)
- [Nginx with dynamic upstreams](https://tenzer.dk/nginx-with-dynamic-upstreams/)




### Директива [proxy_pass](https://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_pass)

```
location /static/ {
  proxy_pass http://127.0.0.1/public/;
}
```

Удаляет часть /static/ из оригинального запроса и добавляет оставшееся в конец проксируемого URI

`/static/assets/style.css` -> `http://127.0.0.1/public/assets/style.css`


```
location /static/ {
  proxy_pass http://127.0.0.1;
}
```

Добавляет весь оргигинальный запрос в конец проксируемого URI.  
В случае изменения оригинального запроса с помощью регулярных выражений передаётся изменёный запрос.  
`/static/assets/style.css` -> `http://127.0.0.1/static/assets/style.css`

```
location /static/ {
  proxy_pass http://127.0.0.1/public$request_uri;
}
```

Добавляет весь оргигинальный запрос в конец проксируемого URI

`/static/assets/style.css` -> `http://127.0.0.1/public/static/assets/style.css`


### Разрешение DNS имён при запуске внутри Docker-контейнера 

Docker использует для сервера имён адрес `127.0.0.11` 
```
location /frontend/ {
  resolver 127.0.0.11 valid=60s;
  proxy_pass http://frontend;
}
```
