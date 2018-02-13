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

### Изменение имени локальной и удаленной ветки 

```shell
git branch -m old_branch new_branch         # Rename branch locally    
git push origin :old_branch                 # Delete the old branch    
git push --set-upstream origin new_branch   # Push the new branch, set local branch to track the new remote
```

Источник: https://gist.github.com/lttlrck/9628955