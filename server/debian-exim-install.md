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
MAIN_TLS_ENABLE = yes
```


Перезагрузить Exim

```shell
service exim4 restart
```

## Материалы

* [Debian Exim Installation](https://wiki.debian.org/Exim#Installation)