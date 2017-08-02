# Обновление программ в Debian

В общем случае достаточно выполнить 

```shell
apt-get update
apt-get upgrade
```

## Установка дополнительных репозиториев

Редактируем файл **/etc/apt/sources.list**

### [Dotdeb](https://www.dotdeb.org)
Есть PHP 7.0 для Jessie, свежие версии MySQL и Redis.

```
deb http://packages.dotdeb.org jessie all
deb-src http://packages.dotdeb.org jessie all
```

### [deb.sury.org](https://deb.sury.org)
Есть PHP 7.1 для Jessie.

```
deb http://packages.sury.org/php jessie all
deb-src http://packages.sury.org/php jessie all
```

## Дополнительная информация
Подробнее о **/etc/apt/sources.list** на [Debian Wiki](https://wiki.debian.org/ru/SourcesList)
