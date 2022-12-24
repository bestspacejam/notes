# Git

### Работа с ветками

```shell
# Список всех веток
git branch -a

# Имя текущей ветки
git branch --show-current

# Список веток которые уже слили в текущую ветку
# (вершины веток содержатся в коммитах текущей ветки)
git branch --merged

# Вытянуть ветку с удалённого репозиторя
git checkout remotes/origin/BRANCH

# Создать локальную ветку
git checkout -b master

# Установить upstream-ветку для master
git branch -u origin/BRANCH

# Скопировать файл из ветки master в текущую
git checkout master -- path/to/file.txt
```

#### Как переименовать ветку на сервере

```shell
# Переименовать ветку локально
git branch -m old_branch new_branch

# Удалить старую ветку на сервере
git push origin :old_branch

# Вытолкнуть новую ветку на сервер
git push --set-upstream origin new_branch
```

### Diff

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

#### Ссылки про diff

- [Difference between git HEAD and the current project state?](https://stackoverflow.com/questions/3293607/difference-between-git-head-and-the-current-project-state)

### Log

```shell
# Выгрузить коммиты за вчерашний день
git log --no-merges --since=yesterday.0:00 --before=yesterday.23:59:59

# Разбить на поля символом табуляции
git log --pretty='format:%H%x09%an%x09%s'

# Задать формат даты
git log -n1 --pretty='format:%cd' --date='format:%Y-%m-%d %H:%M:%S'
```

### Заплатки

```shell
# Сгенерировать заплатку на основе разницы между двумя коммитами
git diff <old_commmit> <new_commit> > my.patch
git apply my.patch
```

Ещё можно сделать: `git cherry-pick -n <other_commit>`.

### Информация об индексе и рабочем каталоге

```shell
# Список неотслеживаемых файлов / директорий
git ls-files --exclude-standard --others --directory --no-empty-directory

# Список изменённых файлов
git ls-files --exclude-standard --modified
```