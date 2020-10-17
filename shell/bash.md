# Bash

### Склеивание массива в строку и разделение на слова с помощью $IFS

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

#### Ссылки
- https://www.gnu.org/software/bash/manual/html_node/Word-Splitting.html
- https://bash.cyberciti.biz/guide/$IFS


### Расширение параметров

#### Удаление части значения переменной

* `${parameter#pattern}` - самый короткий префикс
* `${parameter##pattern}` - самый длинный префикс 
* `${parameter%pattern}` - самый короткий суфикс
* `${parameter%%pattern}` - самый длинный суфикс

```shell
# Вывести имя текущей директории
echo "${PWD##*/}"

# Вывести имя выполняемого скрипта
echo "${0##*/}"
```

#### Изменение регистра

* `${parameter,,pattern}` - все попадающие под шаблон символы приводятся к нижнему регистру
* `${parameter^^pattern}` - все попадающие под шаблон символы приводятся к ВЕРХНЕМУ регистру
* `${parameter,pattern}` - первый символ приводится к нижнему регистру, если он попадает под шаблон
* `${parameter^pattern}` - первый символ приводится к ВЕРХНЕМУ регистру, если он попадает под шаблон

```shell
example=UPPERCASED
echo "${example,,}"
# uppercased
```


#### Косвенная ссылка на переменную

Синтаксис: `${!parameter}`

```shell
bob=user
name=bob
echo ${!name}
# user
```

### Cпециальные параметры

| Модификатор | Поведение |
| - | - |
| * | Все позиционные параметры (одно слово, когда в двойных кавычках) |
| @ | Все позиционные параметры (много слов, когда в двойных кавычках) |
| n | n-й позиционный параметр |
| # | Количество позиционных параметров |
| ? | Код выхода предыдущего не фонового пайплайна |
| - | Текущие флаги оболочки (установленные через set) |
| $ | ID текущего процесса (процесса оболочки) |
| ! | ID последнего запущенного фонового процесса  |
| _ | Последний параметр предыдущей команды |

## Ссылки
* [Shell Parameter Expansion](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html)
