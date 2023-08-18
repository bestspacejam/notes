# FZF

## Параметры

`--delimiter` - регулярное выражение для разделителя полей

## Примеры

### Выделение части данных в предпросмотр

```shell
echo -e 'first line\tfirst preview\nsecond line\tsecond preview' \
  | fzf --delimiter='\t' --with-nth=1 --preview='echo {2}'
```

### Поиск по полю с указанным индексом

```shell
echo -e 'aaa|bbb|ccc\nbbb|ccc|aaa' \
  | fzf --delimiter='\|' --nth=2
```

### Запуск скрипта с выбранным именем файла

```shell
fzf --print0 | xargs -0ron1 /path/to/script
```