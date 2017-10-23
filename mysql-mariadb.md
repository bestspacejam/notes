# MySQL / MariaDB

## Создать root пользователя для всех входящих подключений

```sql
CREATE USER 'root'@'%' IDENTIFIED BY '<password>';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '<password>';
```
