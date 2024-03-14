# Организация доступа по SSH без пароля с помощью закрытого ключа (v2)

## На локальном хосте, откуда будем соединяться с удалённой машиной (выполняется от текущего пользователя)

1. **Сгенерировать пару открытый/закрытый ключ**

```shell
# Команда создаст новые файлы с ключами ~/.ssh/id_rsa и ~/.ssh/id_rsa.pub
ssh-keygen -t rsa -b 4096
```


2. **Скопировать публичный ключ на удалённый сервер**

```
ssh-copy-id <username>@<host>
```


## Ссылки

* [Linux/Mac Tutorial: SSH Key-Based Authentication - How to SSH Without a Password](https://www.youtube.com/watch?v=vpk_1gldOAE) &mdash; видео с ручным копированием публичного ключа и через `ssh-copy-id`
