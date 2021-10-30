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

### Проблемы и решения

**Проблема**

Долгое ожидание запуска билда

**Описание**

Билд может подвисать и стоять в ожидании *(pending)*, если на сервере зарегистрированно несколько раннеров, даже если они сами в данный момент ничем не заняты.

**Решение**

В файле `config.toml` изменить параметр `concurrent` на *(число раннеров)*. То есть если на серевере зарегистрированно три раннера, то указать `concurrent = 3`.

Источник: [Job waiting (pending) for runner too long (#3616) · Issues · GitLab.org / gitlab-runner · GitLab](https://gitlab.com/gitlab-org/gitlab-runner/-/issues/3616)
