# Команды Git

## Ветки

### Список всех веток

```shell
git branch -a
```

### Вытянуть ветку с удалённого репозиторя

```shell
git checkout remotes/origin/BRANCH
```

### Создать локальную ветку

```shell
git checkout -b master
```

### Установить upstream-ветку для master

```shell
git branch -u origin/BRANCH
```