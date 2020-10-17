# Заголовки HTTP для управления режимами безопасности

## Strict-Transport-Security

- <https://developer.mozilla.org/ru/docs/Web/HTTP/Headers/Strict-Transport-Security>

- [«HTTP Strict-Transport-Security» или как обезопасить себя от атак «man-in-the-middle» и заставить браузер всегда использовать HTTPS](https://habrahabr.ru/post/216751/)


Конфигурация Apache (mod SSL):

```
<IfModule mod_ssl.c>
	Header always set Strict-Transport-Security "max-age=63072000; includeSubDomains"
</IfModule>
```


## X-Frame-Options

- <https://developer.mozilla.org/ru/docs/Web/HTTP/Headers/X-Frame-Options>