# Памятка по `git diff`

```
$ git diff
```
Показать изменения в рабочей директории которые не еще не поставлены в следующий коммит (не добавлены в индекс).

```
$ git diff --staged
```
Изменения поставленные в следующий коммит. Показать разницу между индексом и последним коммитом; это то что будет отправлено в следующий коммит при `git commit`.

```
$ git diff HEAD
```
Показать изменения в рабочей директории с момента последнего коммита; всё что будет отправлено в коммит при `git commit -a` (то есть без новых файлов).


## Ссылки

[Difference between git HEAD and the current project state?](https://stackoverflow.com/questions/3293607/difference-between-git-head-and-the-current-project-state)
