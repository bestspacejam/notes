# Склеивание массива в строку и разделение на слова с помощью $IFS

Все элементы массива склеиваются в одно слово с первым символом $IFS в качестве разделителя:

```shell
list=(one two three "four five" "six|seven" "eight,nine")
IFS="|,"
printf " <%s>" "${list[*]}"; echo;
# <one|two|three|four five|six|seven|eight,nine>
```

Каждый элемент массива становится отдельным словом:

```shell
list=(one two three "four five" "six|seven" "eight,nine")
IFS="|,"
printf " <%s>" "${list[@]}"; echo;
# <one> <two> <three> <four five> <six|seven> <eight,nine>
```

Каждый элемент массива раскрывается как отдельное слово котороя в дальнейшем является источником для Word Splitting, Filename Expansion и Quote Removal:
```shell
list=(one two three "four five" "six|seven" "eight,nine")
IFS="|,"
printf " <%s>" ${list[*]}; echo;
# <one> <two> <three> <four five> <six> <seven> <eight> <nine>
```

## Ссылки
- https://www.gnu.org/software/bash/manual/html_node/Word-Splitting.html
- https://bash.cyberciti.biz/guide/$IFS
