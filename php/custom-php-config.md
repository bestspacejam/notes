# Настройка PHP

## Настройка при выполнении через CLI

Если требуется разделить параметры работы PHP запущенного через коммандную строку и с помощью сервера (Apache или FPM).

**Специальный файл конфигурации:**

```
php -c /home/wwwuser/custom-php.ini script.php
```


**Директории для поиска файла конфигурации:**

```
php -c /home/wwwuser/php-config-dir
```

При указании директории будет сначала искаться файл `php-cli.ini`, затем `php.ini`


**Задание дополнительных или изменение загруженных параметров из файла конфигурации:**

```shell
php -d memory_limit=1024M script.php
```


## Дополнительные возможности настройки `php.ini`

В файле конфигурации можно указать переменную окружения из которой будет браться значение параметра

```
memory_limit=${PHP_MEMORY_LIMIT}
```

## Ссылки
- [The configuration file](https://secure.php.net/manual/en/configuration.file.php)
- [Using custom php.ini file with php CLI](http://inchoo.net/dev-talk/custom-php-ini-php-cli/)