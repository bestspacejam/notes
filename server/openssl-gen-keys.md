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

***Извлечение закрытого ключа и сертификата из PFX***

```shell
openssl pkcs12 -in ca.pfx -out key.pem -nodes -nocerts
openssl pkcs12 -in ca.pfx -out cert.pem -nodes -nokeys
```
