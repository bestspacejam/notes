# Разделение строк с помощью $IFS

Файл `ifs.sh`:
```shell
#!/usr/bin/env bash

list=(one two three "four,five")
IFS="|,"

# Склеивание слов из массива в строку разделённую первым символом $IFS.
a="${list[*]}"
echo "$a"
# $ one|two|three|four,five

# Здесь запускается обратный процесс - "parameter expansion", и символы 
# указанные в переменной IFS используются для расширения строки в слова.
echo $a
# $ one two three four five

# Ещё пример расширения строки
b="red|green|blue"
echo $b
# $ red green blue
```

## Ссылки
- https://www.gnu.org/software/bash/manual/html_node/Word-Splitting.html
- https://bash.cyberciti.biz/guide/$IFS
