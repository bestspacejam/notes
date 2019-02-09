# Полезные команды

```shell
# Вывести содержимое файла без закомментированных строк
grep -v "^$\|^#" /etc/dnsmasq.conf

# Посмотреть список ДНС серверов используемых во всех подключениях
nmcli dev show | grep DNS | sed 's/\s\s*/\t/g' | cut -f 2

# Перейти во временную директорию
cd $(mktemp -d) # get an instant temporary directory
```


Скопировано из [EngineerMan / YouTube](https://github.com/engineer-man/youtube):

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

```
