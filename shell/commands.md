### Полезные Shell команды

```shell
# Вывести содержимое файла без закомментированных строк
grep -v "^$\|^#" /etc/dnsmasq.conf

# Посмотреть список ДНС серверов используемых во всех подключениях
nmcli dev show | grep DNS | sed 's/\s\s*/\t/g' | cut -f 2

# Перейти во временную директорию
cd $(mktemp -d) # get an instant temporary directory
```
Источник: [8 super heroic Linux commands that you probably aren't using](https://www.youtube.com/watch?v=Zuwa8zlfXSY)

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

# bonus: exit terminal but leave all processes running
disown -a && exit

# Отсортировать лог-файл по содержимому строки
paste -d' ' <(grep -o -E 'Time:[^,]+' performance.log | cut -d' ' -f2-) performance.log | sort -h
```

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

Обсуждение: https://stackoverflow.com/a/28806991/9215292

### Вызвать команду для каждого переданного аргумента
```shell
#!/usr/bin/env bash
set -e -o pipefail
printf '%s\0' "$@" | xargs -0n1 printf '{%s}\n'
```

### Получить имя директории/файла

```shell
# С помощью команды
basename $PWD

# Через расширение параметра
# Важно: Если путь оканчивается косой чертой - вернётся пустая строка
echo "${PWD##*/}"

# Поддержка путей оканчивающихся косой чертой (/path/to/directory/)
shopt -s extglob
param=${1%%+(/)}
echo "${param##*/}"
```

`##*/` - это [расширение параметра](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html), оно указывает удалить из значения самый длинный найденный шаблон, в данном случае это все символы до последней косой черты.


### Команда cd
В переменной`$PWD` содержится путь до текущей директории

```shell
# Домашняя директория
cd
cd ~
cd $HOME

# Предыдущую директория
cd
cd $OLDPWD
```

### Очистка содержимого от непечатаемых символов

```shell
tr -cd "[:print:]\n" < file1
```
Источник: [Removing all special characters from a string in Bash](https://stackoverflow.com/questions/36926999/removing-all-special-characters-from-a-string-in-bash)

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

### Stdin команды открыт не в терминале

```shell
{ [ ! -t 0 ] && cat; } <<< redirection
```
