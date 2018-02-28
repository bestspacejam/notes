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

### На безопасные методы налагается CORS

- Если заголовок `Content-Type` имеет значение отличное от:

	- `application/x-www-form-urlencoded`
	- `multipart/form-data`
	- `text/plain`

- Если у объекта XMLHttpRequestUpload используемого в запросе зарегистрирован обработчик события.

- Если в запросе используется объект *ReadableStream* (?)


Такие запросы помечаются как **preflighted** (*"предполётные"*). Перед их отправкой клиент отправляет [OPTIONS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/OPTIONS)-запрос для получения с сервера политики обработки кросс-доменных запросов.



## Ссылки

- [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
- [What are idempotent and/or safe methods?](http://restcookbook.com/HTTP%20Methods/idempotency/)
- [Idempotent](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent)