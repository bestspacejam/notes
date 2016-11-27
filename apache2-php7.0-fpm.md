# Настройка работы PHP через FastCGI

Поставить модули Apache:

```bash
apt-get install libapache2-mod-fastcgi
a2enmod fastcgi proxy_fcgi setenvif
```

Поставить PHP FPM:

```bash
apt-get install php7.0-fpm
```

Если PHP стоял как модуль апача - не забыть скопировать измененный **php.ini**:

```bash
cp /etc/php/7.0/apache2/php.ini /etc/php/7.0/fpm/php.ini
```

Проверить статус сервиса FPM:

```bash
service php7.0-fpm status
```

Поменять опцию "SetHandler" в **/etc/apache2/mods-enabled/php7.0.conf** :

```
<FilesMatch ".+\.ph(p[3457]?|t|tml)$">
    #SetHandler application/x-httpd-php
    SetHandler "proxy:unix:/run/php/php7.0-fpm.sock|fcgi://localhost"
</FilesMatch>
```

Перезагрузить Apache и PHP FPM:

```bash
service php7.0-fpm restart
apachectl restart  
```

## Если Apache работает из-под нестандартного пользователя

Изменить владельца **/var/lib/apache2/fastcgi** :

```bash
chown prouser:prouser /var/lib/apache2/fastcgi
```

Прописать в **/etc/php/7.0/fpm/pool.d/www.conf** :

```
user = prouser
group = prouser

listen.owner = prouser
listen.group = prouser
```
