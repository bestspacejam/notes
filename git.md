# Git

## Работа с ветками

### Примеры команд

```shell
# Список всех веток
git branch -a

# Вытянуть ветку с удалённого репозиторя
git checkout remotes/origin/BRANCH

# Создать локальную ветку
git checkout -b master

# Установить upstream-ветку для master
git branch -u origin/BRANCH
```

### Изменение имени локальной и удаленной ветки

```shell
git branch -m old_branch new_branch         # Rename branch locally    
git push origin :old_branch                 # Delete the old branch    
git push --set-upstream origin new_branch   # Push the new branch, set local branch to track the new remote
```

Источник: https://gist.github.com/lttlrck/9628955

### Копирование файлов из ветки в текущую

```shell
git checkout adminpanel
git checkout master -- 'public'
git commit -m "Скопированы файлы из ветки master"
```

Статья: [Quick tip: git-checkout specific files from another branch](http://nicolasgallagher.com/git-checkout-specific-files-from-another-branch/)


## Обзор изменений

### Примеры команд

```shell
# Показать изменения которые ещё не добавлены в индекс (не поставлены в коммит)
git diff

# Изменения поставленные в следующий коммит.
# Покажет разницу между индексом и последним коммитом;
# Это то, что будет отправлено в следующий коммит при `git commit`.
git diff --staged

# Показать изменения в рабочей директории с момента последнего коммита.
# Всё, что будет отправлено в коммит при `git commit -a` (то есть без новых файлов).
git diff HEAD
```

### Создание заплатки

Сгенерировать заплатку на основе разницы между двумя коммитами и применить её.


```
git diff <old_commmit> <new_commit> > my.patch
git apply my.patch
```

Ещё можно сделать `git cherry-pick -n <other_commit>`.

### Ссылки

[Difference between git HEAD and the current project state?](https://stackoverflow.com/questions/3293607/difference-between-git-head-and-the-current-project-state)
