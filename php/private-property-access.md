# Как достать закрытые свойства из объекта

С помощью компонентов:

* [Roave / BetterReflection](https://github.com/Roave/BetterReflection)
* [Ocramius / GeneratedHydrator](https://github.com/Ocramius/GeneratedHydrator)
* [Symfony / The PropertyAccess Component](https://symfony.com/doc/current/components/property_access.html)

С помощью *Object Binding*:

http://sandbox.onlinephpfunctions.com/code/d22589ae24a3f002125536ff876140a3e1f7309c
```php
<?php
class WithPrivateProp
{
    private $prop = [];
 
    public function prop()
    {
        return $this->prop;
    }
}
 
$a = new WithPrivateProp();
 
var_dump($a->prop());
 
(function() {
    $this->prop = 'ola-la';
})->call($a);
 
var_dump($a->prop());
```

http://sandbox.onlinephpfunctions.com/code/eee6987d398f4e731d60611bff622da99dd76329
```php
<?php

class WithPrivateProp
{
    private $prop = "123";
 
    public function prop()
    {
        return $this->prop;
    }
}
 

$foo = new WithPrivateProp();
$haha = \Closure::bind(function ($foo, $prop) {return $foo->$prop; }, null, WithPrivateProp::class);

echo $haha($foo, 'prop');
```
