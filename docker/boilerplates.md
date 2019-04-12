# Конфигурация Docker-сервисов

База данных для тестов:
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
