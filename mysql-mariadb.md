# MySQL / MariaDB

### Простейший экспорт / импорт дампа БД

```shell
# Экспортировать дамп в gzip-файл
mysqldump -u user -p database | gzip > database.sql.gz

# Импортировать дамп из gzip-файла
gunzip < database.sql.gz | mysql -u user -p database

# Экспорт из Docker-контейнера
docker exec -i <mariadb_container> sh -c 'exec mysqldump -u<username> -p<password> <database_name> <table1> <table2>' |
 gzip > dump.sql.gz

# Импорт в Docker-контейнер
docker exec -i <container> mysql -u<username> <database> < metalog_views.sql
```

### Сброс пароля для пользователя

```
# Запустить mariadb с отключеной проверкой разрешений
mysqld_safe --skip-grant-tables &

# Запустить консоль MariaDB
mysql
```

В режиме командной строки:
```sql
USE mysql;
UPDATE user SET authentication_string=PASSWORD('password') WHERE User='root';
FLUSH PRIVILEGES;
quit;
```
`flush privileges` необходимо выполнять после всех прямых манипуляций с таблицой пользователей


### Создание нового пользователя

```sql
CREATE USER 'root'@'%' IDENTIFIED BY 'password';
GRANT ALL ON *.* to 'root'@'%';
```

Если опустить параметр `IDENTIFIED BY`, то пользователь сможет входить без пароля.


### Изменение пароля у существующего пользователя

```sql
SET PASSWORD FOR 'root'@'%'=PASSWORD('password');
```
