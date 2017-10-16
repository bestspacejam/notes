# Сравнение локальной ветки с веткой удалённого репозитория Git

Команда:

```shell
git diff <local branch> <remote>/<remote branch>
```

Пример: `git diff master origin/master`, или `git diff featureA origin/next`

Перед сравнением необходимо загрузить сравниваемую ветку из удалённго репозитория с помощью `git fetch`.

[Ответ на stackoverflow.com](http://stackoverflow.com/a/1801150)