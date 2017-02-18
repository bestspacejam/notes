
#Команды Linux

## Вывести размер каждого из подразделов

```bash
du -sh ./*
```

## Удалить файлы модицированные более суток назад

```bash
find /var/www/site/data/tmp/ -type f -mtime +1 -print0 | xargs -0 rm -f
```
или

```bash
find /var/www/site/data/tmp/ -type f -mtime +1 -delete 2> /dev/null
```
