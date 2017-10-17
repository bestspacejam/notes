# Организация доступа по SSH с использованием аутентификации с помощью закрытого ключа


## На локальном хосте 

1. **Сгенерировать пару открытый/закрытый ключ для OpenSSH**

	*Cоздаём файлы sshkey.pem и sshkey.pem.pub. В файле sshkey.pem.pub содержится код для ~/.ssh/authorized_keys*

	```shell
	ssh-keygen -t rsa -b 2048 -f sshkey.pem -N ''
	```

2. **Ограничить доступ к файлу закрытого ключа**

	*OpenSSH отказывается использовать файл закрытого ключа если у него установлены слишком широкие права доступа.*

	```shell
	chmod 700 sshkey.pem
	```


### Как сбросить сохранённый ключ удалённого хоста

```
ssh-keygen -R <hostname>
```


### Как получить ключ удалённого хоста


```shell
$ ssh-keyscan -t rsa -H bitbucket.org >> ~/.ssh/known_hosts
```

([ссылка на superuser](https://superuser.com/a/1111974))


## На удалённом хосте

1. **Загрузить "sshkey.pem.pub"**

2. **Создать файл "authorized_keys", если ещё не создан.**
	**Внимание!** Команды должны выполняться из под пользователя к которому необходимо предоставить доступ по SSH.
	
	```shell
	mkdir ~/.ssh
	touch ~/.ssh/authorized_keys
	
	chmod 700 ~/.ssh
	chmod 600 ~/.ssh/authorized_keys
	```
	
3. **Добавить публичный ключ в "authorized_keys"**

	```shell
	echo `cat ~/.ssh/sshkey.pem.pub` >> ~/.ssh/authorized_keys
	```

Конфигурация сервера SSH хранится в файле `/etc/ssh/sshd_config`

В случае проблем с аутентификацией смотреть `tail -f /var/log/auth.log`

	
## Ссылки

* [Use Public Key Authentication with SSH](https://www.linode.com/docs/security/use-public-key-authentication-with-ssh) &mdash; вроде неплохой мануал
* [Linux server security best practices](https://support.rackspace.com/how-to/linux-server-security-best-practices/)
* [Как включить DSS-ключи для старых клиентов](https://www.gentoo.org/support/news-items/2015-08-13-openssh-weak-keys.html)