# Git Push

```shell 
git config push.default simple
```
Выталкивать ветку при `git push` только если она явно установлена как отслеживаемая (`--set-upstream-to`) и имена отслеживаемой и локальной ветки совпадают

```shell 
git config push.default current
```
Выталкивать ветку в `origin/HEAD` с текущим именем, даже если она не усктовлена как отслеживаемая

## Документация
[git config](https://mirrors.edge.kernel.org/pub/software/scm/git/docs/git-config.html)
