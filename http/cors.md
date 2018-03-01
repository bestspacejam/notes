# HTTP методы и идемпотентность

> **Идемпотентный** метод не изменяет состояние сервера при повторном к нему обращении.
> Метод не изменяющий состояние сервера, и использующийся только для получения информации, считается *безопасным*.

|     Метод    | Идемпотентный | Безопасный |
|--------------|---------------|------------|
| OPTIONS      | да            | да         |
| GET          | да            | да         |
| HEAD         | да            | да         |
| PUT          | да            | нет        |
| POST         | нет           | нет        |
| DELETE       | да            | нет        |
| PATCH        | нет           | нет        |

## CORS

На безопасные методы налагается **CORS** если они присылают что-то помимо [неконтролируемых пользователем](https://fetch.spec.whatwg.org/#forbidden-header-name) и помеченных как [безопасные](https://fetch.spec.whatwg.org/#cors-safelisted-request-header) заголовков.

**CORS налагается даже на безопасные методы**, если:

- Заголовок `Content-Type` имеет значение отличное от:

	- `application/x-www-form-urlencoded`
	- `multipart/form-data`
	- `text/plain`

- У объекта XMLHttpRequestUpload используемого в запросе зарегистрирован обработчик события.

- В запросе используется объект *ReadableStream* (?)


Такие запросы помечаются как **preflighted** (*"предполётные"*). Перед их отправкой клиент отправляет [OPTIONS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/OPTIONS)-запрос для получения с сервера политики обработки кросс-доменных запросов.


### Заголовки в ответе сервера


- **[Access-Control-Allow-Origin](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Access-Control-Allow-Origin)**
  
    Может принимать значение `Access-Control-Allow-Origin: *` или `Access-Control-Allow-Origin: <address>` (адрес `Origin: <address>` из заголовка запроса).
    
    Необходимо возвращать адрес совпадающий с `Origin` в случае если от клиента пришел заголовок с `Access-Control-Allow-Credentials`, звёздочка в этом случае не поддерживается.
  
- **[Access-Control-Expose-Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Access-Control-Expose-Headers)**

- **[Access-Control-Max-Age](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Access-Control-Max-Age)**

- **[Access-Control-Allow-Credentials](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Access-Control-Allow-Credentials)**

- **[Access-Control-Allow-Methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Access-Control-Allow-Methods)**

- **[Access-Control-Allow-Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Access-Control-Allow-Headers)**



Пример ответа сервера:


```
Access-Control-Allow-Origin: http://localhost:3000
Access-Control-Allow-Methods: POST, GET, OPTIONS
Access-Control-Allow-Headers: Content-Type
Access-Control-Expose-Headers: X-Powered-By, Server
Access-Control-Allow-Credentials: true
Access-Control-Max-Age: 86400
```


## Ссылки

- [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
- [What are idempotent and/or safe methods?](http://restcookbook.com/HTTP%20Methods/idempotency/)
- [Idempotent](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent)