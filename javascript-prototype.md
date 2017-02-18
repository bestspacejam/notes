#__proto__ vs. prototype

`__proto__` is the actual object that is used in the lookup chain to resolve methods, etc. `prototype` is the object that is used to build `__proto__` when you create an object with new:


```javascript
(new Foo).__proto__ === Foo.prototype
(new Foo).prototype === undefined
```

Ответ на StackOverflow:
<http://stackoverflow.com/a/9959753>

Хорошие слайды про прототипы от Джона Резига:
<http://ejohn.org/apps/learn/#64>