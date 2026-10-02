# Памятка по Curl


```shell
# Если надо соединиться с сервером у которого стоит самоподписанный сертификат
curl --cacert  /path/to/CA/cert.file <URL>

# Отключение проверки сертификата при запросе
curl --insecure <URL>

# Конечный адрес ресурса после всех переадресаций
curl -L -w "%{url_effective}\n" -o /dev/null -s <URL>
