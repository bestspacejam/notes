# Библиотека FireEvents.js

## Подписка на события

```javascript
var fe = FireEvents();

// Подписка на событие по имени
fe.on("event-name", function(){ });

// Подписка на события с поиском по регулярному выражению
fe.on(/regexp/, function(){ });

// Подписка на несколько событий
fe.on(["event-name", "another-event-name", /regexp/], function(){ });

// Добавление обработчика события с указанным ярлыком
fe.on("event-name", function(){ }, "event-handler-label");
```

## Удаление обработчика

**Замечание:** Все регистрируемые обработчики событий являются приватными, то есть для удаления необходимо указать ссылку на обработчик или имя ярлыка.

Удаление всех обработчиков события не реализовано намеряно, для защиты чужих обработчиков.

При удалении обработчика по регулярному выражению ищется ссылка на объект регулярного выражения.


```javascript
// Удаление обработчика из всех событий
fe.off(handler_function);

// Удадение обработчиков с указанным ярлыком из всех событий
fe.off("event-handler-label");

// Удадение обработчиков из всех событий с поиском ярлыка по регулярному выражению
fe.off("/regexp/");

// Удаление обработчика из указанных событий
// "/regexp/" здесь это ссылка на регулярное выряжение для поиска события
fe.off(handler_function, "event-name", "another-event-name", /regexp/);
```

Указание списка удаляемых обработчиков и ярлыков:

```javascript
// Удаление несольких обработчиков из всех событий
fe.off([handler_function, another_handler_function, "event-handler-label"]);

// Удаление несольких обработчиков из указанных событий
fe.off([handler_function, another_handler_function, "event-handler-label"], "event-name", "another-event-name", /regexp/);
```

## Самоотписывающиеся обработчики 

```javascript
// Подписка на событие и отписка обработчика после его выполнения
fe.onoff(/regexp/, function(){ });
```


## Вызов события

```javascript
// Вызов события
fe.fire("event-name");

// Вызов события с дополнительными аргументами для обработчиков
fe.fire("event-name", "handler-first-argument", "handler-second-argument", "...etc");

// Вызов нескольких событий
fe.fire(["event-name", "another-event-name"]);
```


## Расширение классов

```javascript
// Добавление реализации событий непосредственно в класс
Object.assign(Car, FireEvents())
car.on("end-of-gas", function(){ /* do stuff */ });

// Расширение в случае конфликта имён
// Таким образом можно создать несколько независимых групп обработчиков
Object.assign(Microwave, {events: FireEvents()})
microwave.events.on("done", function(){ /* do stuff */ });
```