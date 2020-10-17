### Полезные Shell команды


```shell
# 1. redo last command but as root
sudo !!

# 2. open an editor to run a command
ctrl+x+e

# 3. create a super fast ram disk
mkdir -p /mnt/ram
mount -t tmpfs tmpfs /mnt/ram -o size=8192M

# 4. don't add command to history (note the leading space)
 ls -l

# 5. fix a really long command that you messed up
fc

# 6. tunnel with ssh (local port 3337 -> remote host's 127.0.0.1 on port 6379)
ssh -L 3337:127.0.0.1:6379 root@emkc.org -N

# 7. quickly create folders
mkdir -p folder/{sub1,sub2}/{sub1,sub2,sub3}

# 8. intercept stdout and log to file
cat file | tee -a log | cat > /dev/null

# 9. exit terminal but leave all processes running
disown -a && exit

# 10. Отсортировать лог-файл по содержимому строки
paste -d' ' <(grep -o -E 'Time:[^,]+' performance.log | cut -d' ' -f2-) performance.log | sort -h

# 11. Вывести содержимое файла без закомментированных строк
grep -v "^$\|^#" /etc/dnsmasq.conf

# 12. Вывести список всех используемых ДНС серверов
nmcli dev show | grep DNS | sed 's/\s\+/\t/g' | cut -f2

# 12.1. Вывести вторую колонку записи содержащую значение
nmcli dev show | awk '$1 ~ /DNS/ {print $2}'

# 13. Создать и перейти во временную директорию
cd "$(mktemp -d)"

# 14. Проверить, что `stdin` команды открыт не в терминале
{ [ ! -t 0 ] && cat; } <<< redirection

# 15. Вывести строку с поддержкой специальных символов
echo -n $'one\ntwo\nthree'
echo -n -e "one\ntwo\nthree"
printf '%b' "one\ntwo\nthree"

# 16. Вызвать команду для каждого переданного аргумента
printf '%s\0' "$@" | xargs -0n1 printf '{%s}\n'

# 17. Очистка содержимого от непечатаемых символов
tr -cd "[:print:]\n" < file1
```

#### Ссылки
* [8 super heroic Linux commands that you probably aren't using](https://www.youtube.com/watch?v=Zuwa8zlfXSY)
* [Removing all special characters from a string in Bash](https://stackoverflow.com/questions/36926999/removing-all-special-characters-from-a-string-in-bash)

### Вызвать команду для каждой строки из файла в качестве параметра

Описание проблемы, почему аргумент `-L1` не совсем  для этого не подходит:

- `-L1` - вызывает команду для каждой строки, но саму строку разбивает на аргументы по символу пробела.
- `-n1` - вызывает команду для каждого аргумента, после разделения строки.

```shell
# Вариант через трансляцию:
< params.list tr '\n' '\0' | xargs -0 -n1 printf '{%s}\n'

# Вариант через указание разделителя:
xargs -a params.list -n1 -d$'\n' printf '{%s}\n'
```

Скрипт для тестов:
```shell
#!/usr/bin/env sh
printf '-> '
printf '{%s}\n' "$@"
```

Источник: [Make xargs execute the command once for each line of input](https://stackoverflow.com/a/28806991/9215292)


### Получить имя директории/файла

```shell
# С помощью команды
basename "$PWD"

# Через расширение параметра
# Замечание: Если путь оканчивается косой чертой - вернётся пустая строка
echo "${PWD##*/}"

# Поддержка путей оканчивающихся косой чертой (/path/to/directory/)
shopt -s extglob
param=${1%%+(/)}
echo "${param##*/}"
```

`##*/` - удалить из значения самый длинный найденный шаблон. В данном случае это все символы до последней косой черты (см.: [расширение параметра](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html)).


### Навигация в консоли

```shell
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

```shell
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