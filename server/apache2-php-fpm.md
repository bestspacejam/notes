# Настройка работы PHP через FastCGI

Поставить модули Apache:

```shell
apt-get install libapache2-mod-fastcgi
a2enmod fastcgi proxy_fcgi setenvif
```

Поставить PHP FPM:

```shell
apt install php7.1-fpm \
php7.1-common \
php7.1-cli \
php7.1-bcmath \
php7.1-curl \
php7.1-gd \
php7.1-json \
php7.1-mbstring \
php7.1-mysql \
php7.1-opcache \
php7.1-readline \
php7.1-tidy \
php7.1-xml
```

Включить PHP FPM в Apache2:
*(добавляет конфигурацию в "/etc/apache2/conf-enabled/php7.1.conf")*

```shell
a2enconf php7.1-fpm
```

Если PHP стоял как модуль апача - не забыть скопировать измененный **php.ini**:

```shell
cp /etc/php/7.1/apache2/php.ini /etc/php/7.1/fpm/php.ini
```

Проверить статус сервиса FPM:

```shell
service php7.1-fpm status
```


Перезагрузить Apache и PHP FPM:

```shell
service php7.1-fpm restart
apachectl restart  
```

## Если Apache работает из-под нестандартного пользователя

Изменить владельца **/var/lib/apache2/fastcgi** :

```shell
chown prouser:prouser /var/lib/apache2/fastcgi
```

Прописать в **/etc/php/7.1/fpm/pool.d/www.conf** :

```
user = prouser
group = prouser

listen.owner = prouser
listen.group = prouser
```


# Репозитории со свежими версиями PHP

<https://www.dotdeb.org/> - Есть PHP 7.0 для Jessie
<https://deb.sury.org/> - Есть как минимум PHP 7.1 для Jessie


