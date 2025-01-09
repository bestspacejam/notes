## [Открытие портов в Firewalld](https://www.inmotionhosting.com/support/security/how-to-open-a-port-in-firewalld/)

Список стандартных сервисов, со стандартными для них портами:
```shell
firewall-cmd --get-services
```

Если сервис стандартный, его можно добавить в белый список как **постоянный** в текущей  [зоне](https://www.inmotionhosting.com/support/security/how-to-configure-firewalld-basic-commands/#zones):
```shell
sudo firewall-cmd --permanent --add-service=SERVICE
```

Если сервис не стандартный, можно открыть порт **постоянно** указав номер порта и протокол (TCP or UDP):

```shell
sudo firewall-cmd --permanent --add-port=1234/tcp
```

Перезагрузка Firewalld для применения изменений:
```shell
firewall-cmd --reload
```
**Внимание:** Перезагрузка удалит  [–-runtime](https://www.inmotionhosting.com/support/website/security/how-to-configure-firewalld-basic-commands/#runtime) изменения и применит `–permanent` конфигурацию.
## Проверка открытых портов в Firewalld

1. Список открытых сервисов в Firewalld:
```shell
sudo firewall-cmd --list-services
```

2. Список открытых портов в Firewalld:
```shell
sudo firewall-cmd --list-ports
```
