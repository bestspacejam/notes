# Экспортирование объектов из модуля в Node.js (v7.x)

В начале каждого модуля автоматически объявляется конструкция:

```javascript
var exports = module.exports = {};
```

Для экспортирования можно использовать два варианта записи: &quot;Дополняющий&quot; и &quot;Замещающий&quot;.

## Дополняющий
Добавляет ключи в объект `exports` и соответственно в `module.exports`

```javascript
exports.read = function(){ };
exports.write = function(){ };
```

## Замещающий
Заменяет исходный объект новым экспортируемым объектом. При этом `exports` продолжает указывать на исходный объект, но в экспорте не участвует.

```javascript
module.exports = {
	read: function(){ },
	write: function(){ }	
};
```

## В каких случаях использовать `module.exports`

Выдержка из [документации](https://nodejs.org/dist/latest-v7.x/docs/api/modules.html#modules_modules):
> If you want the root of your module's export to be a function (such as a constructor) or if you want to export a complete object in one assignment instead of building it one property at a time, assign it to module.exports instead of exports.

