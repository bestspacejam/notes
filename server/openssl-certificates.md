# OpenSSL - работа с сертификатами

## Добавить самоподписанный сертификат с указанного сервера в доверенные

```shell
sudo -s
apt-get install ca-certificates
SERVERADDRESS=server.bestspacejam.ru
echo | openssl s_client -connect $SERVERADDRESS:443 2>/dev/null | openssl x509 > /usr/share/ca-certificates/$SERVERADDRESS.crt
dpkg-reconfigure ca-certificates
```

## Получение информации о датах сертификата

```shell
echo | openssl s_client -connect server.bestspacejam.ru:2376 2>/dev/null | openssl x509 -noout -dates
```
