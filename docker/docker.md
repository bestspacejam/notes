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

## Копирование файлов из одного `volume` в другой
```shell
docker run --rm -ti -v FROM_VOLUME:/from -v TO_VOLUME:/to busybox cp -av /from/. /to
```

## Список содержимого `volume`

```shell
docker run --rm -ti -v VOLUME_NAME:/data -w /data busybox ls -la
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


## Настройка Docker-сервера

### Увеличение количества создаваемых сетей

По-умолчанию докер через `docker network create` даёт создать не более 30 сетей.
Для того чтобы расширить данное ограничение до **255** необходимо в файле `/etc/docker/daemon.json` указать дополнительную подсеть:

```json
{
   "default-address-pools": [
        {
            "base":"172.17.0.0/12",
            "size":16
        },
        {
            "base":"192.168.0.0/16",
            "size":20
        },
        {
            "base":"10.99.0.0/16",
            "size":24
        }
    ]
}
```

Решение: [How to increase maximum Docker Network on one server? - Stack Overflow](https://stackoverflow.com/questions/41609998/how-to-increase-maximum-docker-network-on-one-server)