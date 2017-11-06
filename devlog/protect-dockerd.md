# Включение авторизации на хосте с Docker Daemon

Исходная инструкция: [Protect the Docker daemon socket](https://docs.docker.com/engine/security/https/#other-modes)


## Корневой сертификат

Определение переменной с именем хоста

```shell
export HOST=production.example.ru
```

Генерация закрытого ключа и сертификата центра сертификации

```shell
openssl genrsa -aes256 -out ca-key.pem 4096
openssl req -new -x509 -days 365 -key ca-key.pem -sha256 -out ca.pem
```


## Сертификат сервера

Генерация закрытого ключа сервера

```shell
openssl genrsa -out server-key.pem 4096
openssl req -subj "/CN=$HOST" -sha256 -new -key server-key.pem -out server.csr
```

Генерация сертификата сервера

В качестве альтернативных имён сервера могут выступать его IP-адреса. Пример: `DNS:production.example.ru,IP:127.0.0.1,IP:10.0.37.3` 

```shell
echo subjectAltName = DNS:$HOST,IP:127.0.0.1 >> extfile.cnf
```

Использовать серверные сертификаты только для серверной аутентификации:

```shell
echo extendedKeyUsage = serverAuth >> extfile.cnf
```

Генерация сертификата сервера подписанного закрытым ключом центра сертификации:

```shell
openssl x509 -req -days 3650 -sha256 -in server.csr -CA ca.pem -CAkey ca-key.pem \
  -CAcreateserial -out server-cert.pem -extfile extfile.cnf
```


## Клиентский сертификат

Генерация закрытого ключа:

```shell
openssl genrsa -out key.pem 4096
```

Генерация запроса подписи клиентского сертификата:

```shell
openssl req -subj '/CN=client' -new -key key.pem -out client.csr
```

Разрещение на использование сертификата для клиентской аутентификации:

```shell
echo extendedKeyUsage = clientAuth >> extfile.cnf
```

Генерация сертификата клиента подписанного закрытым ключом центра сертификации:

```shell
openssl x509 -req -days 3650 -sha256 -in client.csr -CA ~/server-keys/ca.pem -CAkey ~/server-keys/ca-key.pem \
  -CAcreateserial -out cert.pem -extfile extfile.cnf
```

> Сертификаты клиента размещаются в директории `~/.docker`


## После генерации

Копирование корневого сертификата поближе к сертификату клиента:

```shell
cp ~/server-keys/ca.pem ~/client-keys/
```

Удаление файлов запросов на подпись сертификата:

```shell
rm -v ~/server-keys/server.csr \
  ~/client-keys/client.csr
```

Ограничение доступа к файлам ключей:

```
chmod -v 0400 ~/server-keys/ca-key.pem \
  ~/server-keys/server-key.pem \
  ~/client-keys/key.pem
```

Запрет на запись для файлов сертификатов


```shell
chmod -v 0444 ~/server-keys/ca.pem \
  ~/server-keys/server-cert.pem \
  ~/client-keys/cert.pem
```


Создание файла параметров запуска Docker Daemon `/etc/docker/daemon.json`

```json
{
    "debug": false,
    "tls": true,
    "tlscert": "/root/server-keys/server-cert.pem",
    "tlskey": "/root/server-keys/server-key.pem",
    "tlsverify": true,
    "tlscacert": "/root/server-keys/ca.pem",
    "hosts": ["unix:///var/run/docker.sock", "tcp://0.0.0.0:2376"]
}
```

Принято, что Docker с поддержкой TLS должен висеть на 2376 порту


## Настройка запуска Docker Daemon в systemd


Docker Daemon не запустится если у него в параметрах указан параметр совпадающий с ключом в `daemon.json`, в данном случае это ключ "hosts" / `-H`, поэтому необходимо изменить системную процедуру запуска.

Через `systemctl`:

```shell
systemctl edit --full docker.service
```

Через изменение файла `/etc/systemd/system/docker.service`:



```
$ vim /etc/systemd/system/docker.service

# Закомментировано для использования daemon.json
#ExecStart=/usr/bin/dockerd -H fd://
ExecStart=/usr/bin/dockerd
```

Дополнительно: [Переопределение `docker.service` без редактирования основной конфигурации](https://docs.docker.com/engine/admin/systemd/#runtime-directory-and-storage-driver)


## Быстрое создание защищённого сервера

Можно пропустить все эти шаги с ручным созданием сертификатов и настройкой используя **Docker Machine**:

```shell
docker-machine create \
  --driver generic \
  --generic-ip-address=$HOST_IP \
  production
```


## Подключение в Docker Machine уже настроенный сервер

```shell
docker-machine create \
  --driver none \
  --url=tcp://$HOST:2376 \
  production
```

Посмотреть и прописать пути до файлов ключей и сертификатов в `~/.docker/machine/machines/production/config.json`


## Выполнение комманд на удалённом хосте

```shell
docker \
  -H $HOST:2376 \
  --tls \
  --tlsverify \
  --tlscacert ~/.docker/keys/ca.pem \
  --tlscert ~/.docker/keys/cert.pem \
  --tlskey ~/.docker/keys/key.pem \
  ps
```




