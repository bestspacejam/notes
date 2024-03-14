# Базы данных

## Общее

### Нахождение пересекающихся диапазонов

Достаточно сравнить начало первого диапазона с концом второго, и начало второго с концом первого.

**Запоминалка:** Начало меньше конца.

> Если (НАЧАЛО1 < КОНЕЦ2 && НАЧАЛО2 < КОНЕЦ1) значит диапазоны пересекаются.



## MySQL / MariaDB

### Сброс пароля для пользователя

```shell
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

## Резервное копирование

### Логическое

**Простейший экспорт/импорт дампа**

```shell
# Экспортировать дамп в gzip-файл
mysqldump -u user -p database | gzip > database.sql.gz

# Импортировать дамп из gzip-файла
gunzip < database.sql.gz | mysql -u user -p database
```

**Через докер-контейнер**

```shell
# Backup
docker exec CONTAINER /usr/bin/mysqldump -u root --password=root DATABASE > backup.sql

# Restore
cat backup.sql | docker exec -i CONTAINER /usr/bin/mysql -u root --password=root DATABASE
```

Не обязательно выполнять копирование от пользователя `root`, можно завести пользователя с правами:

- `SHOW DATABASES` - если надо вывести список БД
- `SELECT`
- `LOCK TABLES`
- `RELOAD`
- `SHOW VIEW`


### Физическое

1. **Создание пользователя**

```sql
CREATE USER 'mariabackup'@'localhost' IDENTIFIED BY 'password';
GRANT RELOAD, PROCESS, LOCK TABLES, BINLOG MONITOR ON *.* TO 'mariabackup'@'localhost';
```

2. **Копирование файлов базы данных**

```shell
mariabackup --backup \
  --target-dir=/var/mariadb/backup/ \
  --user=mariabackup --password=password
```

### Ссылки

- [Mariabackup Overview](https://mariadb.com/kb/en/mariabackup-overview/#installing-on-linux)
- [Full Backup and Restore with Mariabackup](https://mariadb.com/kb/en/full-backup-and-restore-with-mariabackup/)
- [Container Backup and Restoration](https://mariadb.com/kb/en/container-backup-and-restoration/)