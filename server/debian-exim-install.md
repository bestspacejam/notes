# Установка EXIM4 на Debian

*Проверено на Debian 9*

В оригинале рекомендуется после каждого изменения перезагружать Exim, в данном логе это игнорируется. Если возникнут проблемы и перезагрузка на самом деле необходима - добавить перезагрузки в лог.


```shell
apt install exim4-daemon-heavy
apt install spf-tools-perl
```

Сконфигурировать Exim по минимуму

```shell
dpkg-reconfigure exim4-config
update-exim4.conf
```

Сгенерировать сертификат для TLS

```shell
/usr/share/doc/exim4-base/examples/exim-gencert
```

Изменить файл `/etc/exim4/exim4.conf.template`, добавить перед блоком `MAIN_TLS_ENABLE`:

```
tls_on_connect_ports=465
MAIN_TLS_ENABLE = yes
```

Изменить парамер `SMTPLISTENEROPTIONS` в файле `/etc/default/exim4`:

```
SMTPLISTENEROPTIONS='-oX 465:25 -oP /var/run/exim4/exim.pid'
```


Перезагрузить Exim

```shell
service exim4 restart
```

## Материалы

* [Debian Exim Installation](https://wiki.debian.org/Exim#Installation)
* [НАСТРОЙКА TLS/SSL В EXIM4 НА DEBIAN](http://linuxsnippets.net/ru/node/358)
