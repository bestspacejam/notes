# Экспортирование существующего проекта на GitHub

1. Создать новый пустой репозиторий на GitHub. Не создавать файлы README, лицензию или .gitignore, это можно сделать позднее.
2. Если локальный репозиторий не создан - создать его.

	```shell
	git init
	git add .
	git commit -m "init"
	```

3. [Добавить удалённый репозиторий](https://help.github.com/articles/adding-a-remote/)

	```shell
	git remote add origin "remote repository URL"
	# Sets the new remote
	git remote -v
	# Verifies the new remote URL
	```

4. [Выгрузить изменения](https://help.github.com/articles/pushing-to-a-remote/) из локального репозитория на удалённый

	```shell
	git push origin master
	# Pushes the changes in your local repository up to the remote repository you specified as the origin
	```