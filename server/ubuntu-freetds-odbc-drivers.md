# Установка ODBC и FreeTDS драйвера для работы с MSSQL Server

```
apt install unixodbc unixodbc-dev freetds-dev tdsodbc python-dev
pip install pyodbc
```

После установки появится два файла конфигурации:
`/etc/odbc.ini` и `/etc/freetds/freetds.conf`

## odbc.ini - содержит DSN записи

```
[db01]
Driver=FreeTDS

; Обязательный параметр
; Имя сервера из `freetds.conf` (в квадратных скобках [db01])
Servername=db01

; Дополнительные параметры, замещающие параметры FreeTDS
;TDS_Version=8.0
;Port=1433
;Database=IntraSiteSecurity

```

## freetds.conf - настройки драйвера FreeDTS для отдельного сервера

Подробную информацию по настройке можно посмотреть в `man freetds.conf`

```
[db01]
        host = db01.example.com
        port = 1433
        tds version = 8.0
```


## Подключение через консоль

`isql -v <unixodbc-name> <username> <password>`


## Просмотр информации о файлах конфигурации

`odbcinst -j`


## Ссылки

* [Настраиваем pyodbc в linux ubuntu](http://www.py-my.ru/post/50fe762371144856ca000006)
