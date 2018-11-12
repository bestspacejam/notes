# Шпаргалки по Systemd

Обновление скриптов сервиса
```
systemctl enable docker
systemctl enable docker.socket
```
**Заметка:** после редактирования скриптов надо перезагрузить `systemd`

```
systemctl daemon-reload
```
