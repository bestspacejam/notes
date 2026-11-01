# SSH

## Организация доступа по SSH без пароля

Команды выполняются от текущего пользователя.

```shell
# Генерация приватного ключа в формате ed25519
ssh-keygen -t ed25519

# Генерация приватного ключа в формате RSA размером 4096 байт
ssh-keygen -t rsa -b 4096

# Отправка публичного ключа удалённый хост
ssh-copy-id <username>@<remote-host>
```

Команда `ssh-keygen` создаст новые файлы с ключами `~/.ssh/id_rsa` и `~/.ssh/id_rsa.pub` вместо `rsa` будет название формата ключа.

Формат `ed25519` более современный чем `RSA`.


### Конфигурация сервера: `/etc/ssh/sshd_config`

```
PermitRootLogin prohibit-password
PubkeyAuthentication yes
PasswordAuthentication no
KbdInteractiveAuthentication no
```

После настройки **необходимо перезапустить службу SSH** и попробовать соединиться с сервером в новомм подключении **не выходя из текущей сессии**, чтобы иметь возможность исправить конфигурацию.

```
# Перезапуск службы SSH
sudo systemctl restart sshd

# Подключение по SSH через запрос пароля
ssh -o PreferredAuthentications=password -o PubkeyAuthentication=no <username>@<remote-host>
```

## Ссылки

* [Linux/Mac Tutorial: SSH Key-Based Authentication - How to SSH Without a Password](https://www.youtube.com/watch?v=vpk_1gldOAE) &mdash; видео с ручным копированием публичного ключа и через `ssh-copy-id`
