# Создание удалённого Git-репозитория

1. Инициализировать в директории `~/.gitrepo` чистый репозиторий:

```
git init --bare .gitrepo
```

2. Добавить в репозиторий `post-recieve`-хук и пометить файл как исполняемый:

```
cd .gitrepo/
touch hooks/post-receive
chmod +x hooks/post-receive
```

3. Файл `hooks/post-receive`:

```shell
#!/bin/sh
while read oldrev newrev ref
do
    branch=`echo $ref | cut -d/ -f3`
    git --work-tree=/var/www/html checkout -f $branch
done
```

По мотивам мануала:
https://dev.to/coolgoose/how-to-set-up-a-git-bare-repository-for-web-development-code-pushes-5ca4