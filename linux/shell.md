# Коммандная строка

## xargs

Разбивает стандартный ввод на аргументы по символу пробела или новой строки и передаёт их в указанную функцию.

Пробелы в аргументах могут быть экранированы двойными/одинарными кавычками или обратной косой чертой.

### Параметры `-n` и `-L`

Параметр `-n` ограничивает количество одновременно передаваемых аргументов указанным числом.

Параметр `-L` вызывает программу передавая ей столько аргументов, сколько нашёл их в указанном количестве линий.
Например, для `-L2` и двух линий по 5 аргументов, программа вызовется один раз с 10-ю аргументами.

### Линии и разделение на аргументы

*Линия -- это множество аргументов.*

Строка оканчивающаяся пробелом формирует одну линию аргументов со следующей строкой.

Аргументы на линии разбиваются по символу пробела, пробелы могут экранироваться заключением в кавычки. Пример двух аргументов: `первый-аргумент "второй аргумент"`.

При указанном разделителе (параметр `-d` или `-0`), параметры `-L` и `-n` действуют одинаково.

То есть `xargs` при указанном разделителе находит только один аргумент на линии а дальше уже в зависимости от значения параметра `-L` передаёт указанное количество линий с одним аргументом в программу.


```shell
# Отличие `xargs -L` от `xargs -n`
(echo {1..5}; echo {a..e}) | xargs -n1 sh -c 'echo -n "$0 "; printf "{%s} " "$@"; echo' '->'
(echo {1..5}; echo {a..e}) | xargs -L1 sh -c 'echo -n "$0 "; printf "{%s} " "$@"; echo' '->'
```

Для разделения на вызовы программы, по одному вызову на строку ввода, параметр `-L` лучше не использовать.

Обсуждение проблемы: [Make xargs execute the command once for each line of input](https://stackoverflow.com/a/28806991/9215292)

### Примеры

```shell
# Вызов команды для каждой строки из файла в качестве параметра
xargs -a params.txt -n1 -d$'\n' printf '{%s}\n'

# Имена файлов могут содержать символы переноса строк, поэтому
# для команды find лучше использовать параметр -print0
find / -maxdepth 1 -print0 | xargs -0 -n1 printf '{%s}\n'

# Удаление файлов изменённых более суток назад
find . -type f -mtime +1 -print0 | xargs -0 rm -f
```

## printf

### Дополнение длины и обрезка строки
```
$ printf '|%*.*s|\n' 4 2 123
|  12|

$ printf '|%4.2s|\n' 123
|  12|
```
Звёздочка (`*`) в формате означает, что значение придёт из аргумента.

### Ссылки
* [printf — Википедия](https://ru.wikipedia.org/wiki/Printf)
* [printf format string - Wikipedia](https://en.wikipedia.org/wiki/Printf_format_string)

## Bash / Shell Parameter Expansion

### Удаление префикса/суфикса

```
${parameter#pattern}
Удаление из начала строки первого найденого шаблоном совпадения

${parameter##pattern}
Жадное удаление начала строки (шаблон * будет искать самое длинное совпадение)

${parameter%pattern}
Удаление из конца строки первого найденого шаблоном совпадения

${parameter%%pattern}
Жадное удаление конца строки (шаблон * будет искать самое длинное совпадение)
```

### Изменение регистра

```
${parameter,,pattern} - все попадающие под шаблон символы приводятся к нижнему регистру
${parameter^^pattern} - все попадающие под шаблон символы приводятся к ВЕРХНЕМУ регистру
${parameter,pattern} - первый символ приводится к нижнему регистру, если он попадает под шаблон
${parameter^pattern} - первый символ приводится к ВЕРХНЕМУ регистру, если он попадает под шаблон
```

### Примеры использования

```shell
# Имя текущей директории
echo "${PWD##*/}"

# Имя выполняемого скрипта
echo "${0##*/}"

# Путь до директории выполняемого скрипта
echo "${0%/*}"
dirname -- "$0"

# Изменить регистр значения на нижний:
example=UPPERCASED
echo "${example,,}"

# Получить значение переменной "bob":
bob=user
name=bob
echo ${!name}
```

### Дополнительные материалы

- [Shell Parameter Expansion (Bash Reference Manual)](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html#Shell-Parameter-Expansion)

## Bash / Cпециальные параметры

```
$* - Все позиционные параметры (одно слово, когда в двойных кавычках)
$@ - Все позиционные параметры (много слов, когда в двойных кавычках)
$n - n-й позиционный параметр
$# - Количество позиционных параметров
$? - Код выхода предыдущего не фонового пайплайна
$- - Текущие флаги оболочки (установленные через set)
$$ - ID текущего процесса (процесса оболочки)
$! - ID последнего запущенного фонового процесса
$_ - Последний параметр предыдущей команды
```

## Интересные команды

```shell
# Выполнить предыдущую команду как суперпользователь
sudo !!

# Открыть редактор для ввода комманды
ctrl+x+e

# Открыть редактор для изменения и выполнения предыдущей комманды
fc

# Не сохранять команду в истории (пробел перед командой)
 ls -l

# Выполнить команду игноририруя алиас
\ls

# Выполнить команду игнорируя алиасы и объявленные функции
# (будут использоваться только пути поиска указанные в $PATH)
command ls

# Созать быстрый RAM-диск
mkdir -p /mnt/ram
mount -t tmpfs tmpfs /mnt/ram -o size=8192M

# tunnel with ssh (local port 3337 -> remote host's 127.0.0.1 on port 6379)
ssh -L 3337:127.0.0.1:6379 root@emkc.org -N

# Создать несколько вложенных директорий
mkdir -p folder/{sub1,sub2}/{sub1,sub2,sub3}

# intercept stdout and log to file
cat file | tee -a log | cat > /dev/null

# Выйти из терминала, но оставить все процессы запущенными
disown -a && exit

# Отсортировать лог-файл по содержимому строки
paste -d' ' <(grep -o -E 'Time:[^,]+' performance.log | cut -d' ' -f2-) performance.log | sort -h

# Вывести содержимое файла без закомментированных строк
grep -v "^$\|^#" /etc/dnsmasq.conf

# Вывести список всех используемых ДНС серверов
nmcli dev show | awk '$1 ~ /DNS/ {print $2}'

# Создать временную директорию и перейти в неё
cd -- "$(mktemp -d)"

# Проверить, что `stdin` команды открыт не в терминале
{ [ ! -t 0 ] && cat; } <<< redirection

# Вывести строку с поддержкой специальных символов
echo -n $'one\ntwo\nthree'
echo -n -e "one\ntwo\nthree"
printf '%b' "one\ntwo\nthree"

# Вызвать команду для каждого переданного аргумента
printf '%s\0' "$@" | xargs -0n1 printf '{%s}\n'

# Очистка содержимого от непечатаемых символов
tr -cd "[:print:]\n" < file1

# Получить имя исполняемого файла без вызова basename
echo "${0##*/}"

# Массовое переименование файлов
find ./files -name '*.md' -print0 | sed -z 'p;s/md$/mdx/' | xargs -0rn2 mv --

# Получить время выполнения процессов с указанным именем
ps -o time= -C chrome

# Показать строки содержащиеся только в file2.txt
comm -13 <(sort -u file1.txt) <(sort -u file2.txt)

# Удаление файлов изменёных более суток назад
find . -type f -mtime +1 -delete 2> /dev/null

# Вывести размер содержимого по каждому из подразделов
du -sh ./*

# Сделать файл неизменяемым
sudo chattr -i file.txt

# Выставить всем файлам права 644, а директориям 755
chmod -R u=rw,go=r,a+X ./dirname

# Проверить страницу на содержимое
# "tac | tac" нужен для полной загрузки содержимого страницы и передачи в grep
# Описание проблемы: https://stackoverflow.com/a/28879552/9215292
curl "url" | tac | tac | grep -qs foo

# Получить http статус сайта
curl -LsI -o /dev/null -w '%{http_code}\n' 'url'

# Удалить из файла все строки, кроме 100 последних
tail -n100 access.log | sponge access.log

# Ожидать нажатия любой клавиши
read -n1 -s -p $'Press any key to continue...\n'

# Проверка на конец месяца
test $(date -d tomorrow +%-d) -eq 1 && echo "today end of the month"

# Повторить символ 60 раз
printf '%*s\n' 60 | tr ' ' '='
tr '\0' '=' </dev/zero | head -c60 | xargs

# Список процессов использующих указанный путь
lsof | grep /mnt/path

# Убрать начальную директорию из вывода find
find -type f -printf '%P\n'

# Список объявленных функций (в рамках текущей подоболочки/скрипта)
declare -F | cut -d' ' -f3

# Повторить символ или строку N-раз
yes = | head -n10 | tr -d '\n'

# Список имён поддиректорий
find -mindepth 1 -maxdepth 1 -type d -printf '%f\0'

# Удаление всех строк, кроме трёх последних
seq 10 | head -n-3
```

#### Ссылки
* [8 super heroic Linux commands that you probably aren't using](https://www.youtube.com/watch?v=Zuwa8zlfXSY)
* [Removing all special characters from a string in Bash](https://stackoverflow.com/questions/36926999/removing-all-special-characters-from-a-string-in-bash)


### Подсчёт повторяющихся строк в файле

```bash
alias sus='sort | uniq -c | sort -n'
```

Пример использования:
```bash
cut -d ' ' -f6- /var/log/syslog | sus -r | less
```


### Копирование файлов `.php` в структуру директорий PSR-4

```bash
grep -PorH --include='*.php' '^namespace \K[^;]+' ./src \
| sed 's/\\/\//g' \
| while IFS=':' read -r file path; do
    mkdir -p -- "./dst/${path}"
    cp -- "${file}" "${_}/"
  done
```

### Экранирование и удаление экранирования строк

```
$ bash -c "$@" "printf '%s' $(printf '%q' $'new\nline.txt')"
new
line.txt
```

### Подсчёт количества страниц в PDF

#### Через Ghostscript

```bash
gs \
  -dQUIET \
  -dNODISPLAY \
  -c "(file.pdf) (r) file runpdfbegin pdfpagecount = quit"
```

#### Через pdfinfo (poppler-utils)

```bash
pdfinfo "file.pdf" | awk '$1=="Pages:" {print $2; exit}'
```

### Получение текстового содержимого web-страницы

```bash
w3m -dump -cols 99999 example.ru
```

### Навигация в консоли

```bash
# Перейти в домашнюю директорию
cd
cd ~

# Вернуться в предыдущую директорию
cd -
```

### Переменные окружения

```
$HOME - домашняя директория 
$PWD - путь до текущей директории 
$OLDPWD - путь до предыдущей директории 
```

### Использование DEBUG trap для отладки скрипта

```bash
trap '(read -p "[$BASH_SOURCE:$LINENO] $BASH_COMMAND?")' DEBUG
var=2
echo $((var+2))
```

### Склеивание массива в строку и разделение на слова

```bash
IFS="| "
list=(one "two three" four)

# Все элементы массива склеиваются в одно слово с первым символом IFS в качестве разделителя:
# <one|two three|four>
printf " <%s>" "${list[*]}"; echo;

# Каждый элемент массива становится словом, IFS не используется:
# <one> <two three> <four>
printf " <%s>" "${list[@]}"; echo;

# Каждый элемент массива раскрывается как отдельное слово которое 
# в дальнейшем является источником для Word Splitting, Filename Expansion и Quote Removal:
# <one> <two> <three> <four>
printf " <%s>" ${list[*]}; echo;
```

#### Ссылки
- https://www.gnu.org/software/bash/manual/html_node/Word-Splitting.html
- https://bash.cyberciti.biz/guide/$IFS


### Удаление переносов строк из имён файлов

```bash
# (медленно)
find . -type f -name $'*\n*' -print0 \
| while IFS= read -rd '' file; do
    mv "$file" "$(printf %s "$file" | tr -d '\n')"
  done

# (быстро)
find . -type f -name $'*\n*' -exec sh -c 'mv "$1" "$(printf %s "$1" | tr -d "\n")"' sh "{}" \;

# (очень медленно)
find . -type f -name $'*\n*' -exec rename -v 's/\n//g' "{}" \;

# (очень быстро)
find . -type f -name $'*\n*' -print0 | rename -v -0 's/\n//g'
```

**Примечание:**

Если перенос строки содержится также и в имени директории, в которой лежит файл, то данные решения не сработают.

### Преобразование простого списка в JSON (`column`)

```bash
column \
  --separator=':' \
  --table \
  --table-columns='login,password,uid,gid,gecos,home,shell' \
  --table-name='users'\
  --json \
  /etc/passwd
```

### Отображение файла `/etc/fstab` в виде таблицы (`column`)
```bash
grep -v '^#' /etc/fstab \
  | column -t -N 'FILE SYSTEM,MOUNT POINT,TYPE,OPTIONS,DUMP,PASS' -R 'DUMP,PASS'
```

### Запись взаимодействия с терминалом (`script`)

```shell
# Запись терминальной сессии
script script.log

# Выполнение и запись финального результата вывода комманды
script -c 'top' top.log

# Запись с временными метками 
script script.log -t=time.log
scriptreplay -s script.log --timing=time.log
```

### Построчное объединение текстовых файлов

`cat` объединяет файлы "как есть" - без учёта наличия переноса строки в конце файла.

То есть строка из файла без завершающего `\n` станет началом строки из следующего файла.

```bash
# Символ переноса добавляется во все строки переданных файлов
awk 1 *

# В последнюю строку последнего файла символ переноса строки не добавляется
sed '' *

# Символ переноса добавляется во все строки
grep -h '' *

# Объединение большого количества файлов через указание директории
grep -Rh '' ./
```