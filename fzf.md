# FZF

### Выделение части данных в предпросмотр

```shell
echo -e 'first line\tfirst preview\nsecond line\tsecond preview' \
  | fzf --delimiter='\t' --with-nth=1 --preview='echo {2}'
```

### Искать только по полю с указанным индексом

```shell
echo -e 'aaa|bbb|ccc\nbbb|ccc|aaa' \
  | fzf --delimiter='\|' --nth=2
```

### Параметры

`--delimiter` - регулярное выражение для разделителя полей