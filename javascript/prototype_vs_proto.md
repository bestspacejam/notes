# Prototype vs. __proto__

```javascript
// "__proto__ VS. prototype in JavaScript":
// https://stackoverflow.com/questions/9959727/proto-vs-prototype-in-javascript

var Creature = function(){ console.log('Creature'); };
var Animal   = function(){ console.log('Animal'); };
var Squirel  = function(){ console.log('Squirel'); };
var Rabbit   = function(){ console.log('Rabbit'); };
var Bunny    = function(){ console.log('Bunny'); };

Animal.prototype = Object.create(Creature.prototype);
Animal.prototype.constructor = Animal;

Rabbit.prototype = Object.create(Animal.prototype);
Rabbit.prototype.constructor = Rabbit;

Squirel.prototype = Object.create(Animal.prototype);
Squirel.prototype.constructor = Squirel;

Bunny.prototype = Object.create(Rabbit.prototype);
Bunny.prototype.constructor = Bunny;

var bunny_squirelized = new Bunny();

// Меняем прототип созданного объекта на не участвующий в дальнейшем наследовании
bunny_squirelized.__proto__ = Squirel.prototype;

console.log("Changing __proto__ to a Squirel.prototype");
console.log(bunny_squirelized);
console.log("instanceof Rabbit: "  + (bunny_squirelized instanceof Rabbit));
console.log("instanceof Squirel: " + (bunny_squirelized instanceof Squirel));

var bunny = new Bunny();

console.log(bunny);
console.log("instanceof Rabbit: "  + (bunny instanceof Rabbit));
console.log("instanceof Squirel: " + (bunny instanceof Squirel));
```
