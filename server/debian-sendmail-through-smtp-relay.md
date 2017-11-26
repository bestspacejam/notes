# Отправка писем через сторонний SMTP сервер

## Установка клиента для отправки писем

```shell
apt update
apt install ssmtp
```


## Настройка

Добавляем в файл `/etc/ssmtp/ssmtp.conf` параметры:

```shell
root=username@gmail.com
mailhub=smtp.gmail.com:465
rewriteDomain=gmail.com
AuthUser=username
AuthPass=password
FromLineOverride=YES
UseTLS=YES
```


Для отправки через relay-сервер висяший на 25 порту без аутентификации и шифрования:

```shell
# The person who gets all mail for userids < 1000
# Make this empty to disable rewriting.
root=webuser@mail.example.com

# The place where the mail goes. The actual machine name is required no
# MX records are consulted. Commonly mailhosts are named mail.domain.com
mailhub=mail.example.com:25

# Where will the mail seem to come from?
rewriteDomain=mail.example.com

# Are users allowed to set their own From: address?
# YES - Allow the user to specify their own From: address
# NO - Use the system generated From: address
FromLineOverride=YES

UseTLS=NO
```


## Отправка сообщения

```
ssmtp -v user@mail.ru << 'EOF'
To: user@mail.ru
From: site@example.com
Subject: Sent from a terminal!

Your content goes here. Lorem ipsum dolor sit amet, consectetur adipisicing.
(Notice the blank space between the subject and the body.)
EOF
```


## Справочные ресурсы

[ssmtp(8) - Linux man page](https://linux.die.net/man/8/ssmtp)
[How to send mail from the command line?](https://askubuntu.com/questions/12917/how-to-send-mail-from-the-command-line)
[Can I set up system mail to use an external SMTP server?](https://unix.stackexchange.com/questions/36982/can-i-set-up-system-mail-to-use-an-external-smtp-server)