# Библиотека FireEvents.js (v0)

## Подписка на события

```javascript
var fe = FireEvents();

// Подписка на событие по имени
fe.on("event-name", function(){ });

// Подписка на несколько событий
fe.on(["event-name", "another-event-name"], function(){ });
```

## Удаление обработчика

**Замечание:** Все регистрируемые обработчики событий являются приватными, то есть для удаления необходимо указать ссылку на обработчик.

Удаление всех обработчиков события не реализовано намеряно, для защиты чужих обработчиков.

```javascript
// Удаление обработчика из всех событий
fe.off(handler_function);

// Удаление обработчика из указанных событий
fe.off(handler_function, "event-name", "another-event-name");
```

Указание списка удаляемых обработчиков и ярлыков:

```javascript
// Удаление несольких обработчиков из всех событий
fe.off([handler_function, another_handler_function]);

// Удаление несольких обработчиков из указанных событий
fe.off([handler_function, another_handler_function], "event-name", "another-event-name");
```

## Самоотписывающиеся обработчики 

```javascript
// Подписка на событие и отписка обработчика после его выполнения
fe.onoff("event-name", function(){ });
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