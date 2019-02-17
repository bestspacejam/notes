# MySQL / MariaDB

Создание пользователя root для всех входящих подключений

```sql
CREATE USER 'root'@'%' IDENTIFIED BY '<password>';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '<password>';
```

Простейший экспорт / импорт дампа БД

```shell
# Экспортировать дамп в gzip-файл
mysqldump -u user -p database | gzip > database.sql.gz

# Импортировать дамп из gzip-файла
gunzip < database.sql.gz | mysql -u user -p database
```
