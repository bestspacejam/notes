# Docker

## Удаление повисших образов

**Повисшие образы* - это образы оставшиеся после сборки нового образа с тем же именем.

```shell
docker images --quiet --filter="dangling=true" | xargs --no-run-if-empty docker rmi
docker image prune --force
```

## Удаление неиспользуемых хранилищ созданных автоматически

```shell
docker volume ls -q -f "dangling=true" | grep -E '^[[:xdigit:]]{64}$' | xargs --no-run-if-empty docker volume rm
```



## Список загруженных репозиториев образов

```shell
docker images --format "{{.Repository}}" | sort -u
```


## MySQL

### Тестовый сервер `docker-compose.yml`

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

### Импорт дампа

```shell
docker-compose exec -T db mysql -uroot < databases-backup.sql
```


## Docker in Docker

С поддержкой TLS `dockerd` запускается на `2376` порту, без TLS на `2375`


### Создание контекста

```shell
docker run -d \
  --rm \
  --privileged \
  --name dind \
  -e "DOCKER_TLS_CERTDIR=" \
  -p 2375:2375 \
  docker:19-dind

docker context create \
  dind \
  --docker "host=tcp://127.0.0.1:2375" \
  --default-stack-orchestrator swarm
```


### Запуск с самоподписанным сертификатом

```shell
docker run -d \
  --rm \
  --privileged \
  --name dind \
  --network dind-network \
  --network-alias docker \
  -v docker-certs-client:/certs/client \
  docker:19-dind

docker run \
  --rm \
  --network dind-network \
  -v docker-certs-client:/certs/client:ro \
  docker:19 version
```


### Запуск с отключенным TLS

```shell
docker run -d \
  --rm \
  --privileged \
  --name dind \
  --network dind-network \
  --network-alias docker \
  -e "DOCKER_TLS_CERTDIR=" \
  docker:19-dind

docker run \
  --rm \
  --network dind-network \
  -e "DOCKER_TLS_CERTDIR=" \
  docker:19 version
```
