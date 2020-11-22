# Docker

## Удаление всех повисших образов

Образы оставшиеся после сборки нового образа с именем которое уже использовалось до этого

```shell
docker images --quiet --filter="dangling=true" | xargs --no-run-if-empty docker rmi
docker image prune --force
```


## Тестовый сервер базы данных

Файл `docker-compose.yml`:

```yaml
version: "3"
services:
  db:
    image: mariadb
    volumes:
      - ./data:/var/lib/mysql
    environment:
      MYSQL_ALLOW_EMPTY_PASSWORD: 'yes'
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    ports:
      - 8080:80
```

Импорт дампа в сервис:

```shell
docker-compose exec -T db mysql -uroot < databases-backup.sql
```
