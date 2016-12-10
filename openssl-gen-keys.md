# Генерация закрытого ключа и сертификата
Сетификат подписывается сгенерированным ключом

```bash
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365
```

- <https://stackoverflow.com/questions/10175812/how-to-create-a-self-signed-certificate-with-openssl>
- <https://www.openssl.org/docs/apps/req.html>


**Извлечение открытого ключа из пары закрытого/открытого:**

```bash
openssl rsa -in key.pem -pubout -out pubkey.pem
```

- <https://stackoverflow.com/questions/5244129/use-rsa-private-key-to-generate-public-key>


**Удаление пароля закрытого ключа**

```
openssl rsa -in key.pem -out privkey.pem
```