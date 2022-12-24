# GitLab

## GitLab Runner

Файл конфигурации: `/etc/gitlab-runner/config.toml`

### Основные комманды

Список зарегистрированных раннеров:

```shell
sudo gitlab-runner list
```

Проверка состояния раннеров:

```shell
sudo gitlab-runner verify
```

### Запуск из образа

```shell
docker run --rm \
    --name gitlab-runner \
    -u "$(id -u):$(getent group docker | cut -d: -f3)" \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v "$PWD/config.toml:/etc/gitlab-runner/config.toml" \
    -v "$PWD:$PWD" \
    -w "$PWD" \
    gitlab/gitlab-runner \
    exec docker --docker-privileged build
```

### Проблемы и решения

**Проблема**

Долгое ожидание запуска билда

**Описание**

Билд может подвисать и стоять в ожидании *(pending)*, если на сервере зарегистрированно несколько раннеров, даже если они сами в данный момент ничем не заняты.

**Решение**

В файле `config.toml` изменить параметр `concurrent` на *(число раннеров)*. То есть если на серевере зарегистрированно три раннера, то указать `concurrent = 3`.

Источник: [Job waiting (pending) for runner too long (#3616) · Issues · GitLab.org / gitlab-runner · GitLab](https://gitlab.com/gitlab-org/gitlab-runner/-/issues/3616)
