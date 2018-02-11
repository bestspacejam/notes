# Наследование в JavaScript

```javascript
function Animal(){ console.log("Animal Constructor"); }
function Rabbit(){ console.log("Rabbit Constructor"); }

// "constructor" автоматически добавляется JavaScript-ом в прототип при объявлении функции
// и может использоваться используется для вызова конструктора, например родительского класса
// при наследовании.

// Object.create вместо прямого присваивания объекта прототипа копирует его свойства в новый,
// что исключает влияние изменений прототипа родительского класса на дочерние классы.
Rabbit.prototype = Object.create(Animal.prototype);

// Если не поменять свойство "constructor" после полного замещения свойств прототипа
// свойствами родительского класса - конструктор текущего класса будет указывать 
// на конструктор родительского, что не очень удобно для последующего наследования 
// и вызова самого себя.
Rabbit.prototype.constructor = Rabbit;

var rabbit = new Rabbit();

console.log(Rabbit.prototype.constructor);
console.log(rabbit.__proto__.constructor);
console.log(rabbit.constructor);
```