# Получение предыдущей версии файла из Git

```shell
git show HEAD^:file.txt > file-old.txt
```

Путь до файла указывается относительно корня проекта (там, где находится `.git/`).

Для поиска файла относительно текущей рабочей директории, необходимо указать "`./`" в начале пути до файла, например `HEAD^:./file.txt`

Ответ на Stackoverflow: http://stackoverflow.com/a/888623