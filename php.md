# PHP

## Функции

### intdiv

Возвращает целое число на которое может быть разделено указанное число с минимальным остатком. Остаток от деления при этом находится через "%".

```php
echo intdiv(5, 2); // 2
echo 5 % 2; // 1
```


## Файл конфигурации и настройка

### Настройка при выполнении через CLI

Если требуется разделить параметры работы PHP запущенного через коммандную строку и с помощью сервера (Apache или FPM).

```shell
# Файл конфигурации
php -c /home/wwwuser/custom-php.ini script.php

# Директория для поиска файла конфигурации
# Cначала ищется файл `php-cli.ini`, затем `php.ini`
php -c /home/wwwuser/php-config-dir

# Изменение отдельных параметров конфигурации
php -d memory_limit=1024M script.php
```

### Изменение `php.ini` через переменные окружения

В файле конфигурации можно указать имя переменной окружения содержащей значение параметра

```
memory_limit=${PHP_MEMORY_LIMIT}
```

#### Ссылки
- [The configuration file](https://secure.php.net/manual/en/configuration.file.php)
- [Using custom php.ini file with php CLI](http://inchoo.net/dev-talk/custom-php-ini-php-cli/)

## Доступ к закрытым свойствам объекта

### Через [Closure Binding](https://secure.php.net/manual/ru/class.closure.php)

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
http://sandbox.onlinephpfunctions.com/code/d22589ae24a3f002125536ff876140a3e1f7309c

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
http://sandbox.onlinephpfunctions.com/code/eee6987d398f4e731d60611bff622da99dd76329

### Компоненты для доступа к закрытым свойствам

* [Roave / BetterReflection](https://github.com/Roave/BetterReflection)
* [Ocramius / GeneratedHydrator](https://github.com/Ocramius/GeneratedHydrator)
* [Symfony / The PropertyAccess Component](https://symfony.com/doc/current/components/property_access.html)
