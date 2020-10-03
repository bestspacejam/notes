## Заметки о Bash

### Изменение регистра значения переменной

Через синтаксис [Shell Parameter Expansion](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html)

```
# example=UPPERCASED
# echo ${example,,}
uppercased
```

Описание парметров:

- `,,` - все подходящие символы приводятся к нижнему регистру
- `^^` - все подходящие символы приводятся ВЕРХНЕМУ регистру
- `,` - приведение первого символа к нижнему регистру если он подходит под шаблон
- `^` - приведение первого символа к ВЕРХНЕМУ регистру если он подходит под шаблон

### Очистка содержимого от непечатаемых символов

```shell
tr -cd "[:print:]\n" < file1
```

[Removing all special characters from a string in Bash](https://stackoverflow.com/questions/36926999/removing-all-special-characters-from-a-string-in-bash)


### Использование DEBUG trap для отладки скрипта

```shell
#!/usr/bin/env bash
trap '(read -p "[$BASH_SOURCE:$LINENO] $BASH_COMMAND?")' DEBUG

var=2
echo $((var+2))
```
Пример:
```
$ ./trap.sh
[./trap.sh:4] var=2?
[./trap.sh:5] echo $((var+2))?
```
