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

# Экспорт из Docker-контейнера
docker exec -i <mariadb_container> sh -c 'exec mysqldump -u<username> -p<password> <database_name> <table1> <table2>' |
 gzip > dump.sql.gz

# Импорт в Docker-контейнер
docker exec -i <container> mysql -u<username> <database> < metalog_views.sql
```
