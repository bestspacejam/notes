# Работа с ключами

## Генерация закрытого ключа и сертификата

*Сетификат подписывается сгенерированным ключом*

```bash
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365
```

- [How to create a self-signed certificate with openssl?](https://stackoverflow.com/questions/10175812/how-to-create-a-self-signed-certificate-with-openssl)
- [Опции параметра "openssl req"](https://linux.die.net/man/1/req)


**Извлечение открытого ключа из пары закрытого/открытого:**

```bash
openssl rsa -in key.pem -pubout -out pubkey.pem
```

- [Use RSA private key to generate public key?](https://stackoverflow.com/questions/5244129/use-rsa-private-key-to-generate-public-key)


**Удаление пароля закрытого ключа:**

```
openssl rsa -in key.pem -out privkey.pem
```

**Извлечение закрытого ключа и сертификата из PFX**

```shell
openssl pkcs12 -in ca.pfx -out key.pem -nodes -nocerts
openssl pkcs12 -in ca.pfx -out cert.pem -nodes -nokeys
```


## Генерация закрытого и открытого ключа

```shell
# Генерация пары закрытый/открытый ключ в формате RSA
openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048

# Извлечение из закрытого ключа, открытого, в формате OpenSSH
ssh-keygen -f private_key.pem -y > public_ssh_key.pub
```

## Генерация закрытого ключа и самоподписанного сертификата 

```shell
openssl req -x509 -newkey rsa:2048 -keyout private-key.pem -out certificate.pem -days 365
```

## Конвертация PFX в PEM формат

```shell
openssl pkcs12 -in file.pfx -out file.pem
```


## Генерация клиентского сертификата в P12 на основе закрытого ключа корневого сертификата

Используется для реализации аутентификации по сертификату

```shell
openssl pkcs12 -export -in client/cert.pem -inkey client/key.pem -certfile ca.pem -name "Client" -out client/cert.p12
```


## Объединение конечного сертификата с промежуточными

**Принцип объединения:** Сначала идёт сертификат конечного домена, далее промежуточные сертификаты CA, самым последним идёт корневой.

### Примеры

Создание бандла для использования в директиве "ssl_certificate" Nginx-а:

```shell
cat www.example.com.crt bundle.crt > www.example.com.chained.crt
```

Создание бандла для использования в директиве "SSLCACertificateFile" Apache2 (пример для [сертификатов COMODO][1]):

```shell
cat ComodoRSAAddTrustCA.crt "[ComodoRSADomain|Organization|ExtendedvalidationSecureServerCA]".crt AddTrustExternalCARoot.crt > intermediate.ca-bundle
```

## Генерация дайджеста
*Взято из [документации по SRI](https://www.w3.org/TR/SRI/):*

```shell
echo -n "alert('Hello, world.');" | openssl dgst -sha384 -binary | openssl base64 -A
```

[1]: https://support.comodo.com/index.php?/comodo/Knowledgebase/Article/View/620/0/which-is-root-which-is-intermediate