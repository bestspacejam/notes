# Полезные команды

```
grep -v "^$\|^#" /etc/dnsmasq.conf
```
Вывести содержимое файла без закомментированных строк

```
nmcli dev show | grep DNS | sed 's/\s\s*/\t/g' | cut -f 2
```
Посмотреть список ДНС серверов используемых во всех подключениях

```
cd $(mktemp -d) # get an instant temporary directory
```
Перейти во временную директорию
