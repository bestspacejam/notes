# Git Push

```shell 
git config push.default upstream
```
Выталкивать при `git push` в любую ветку установленую в качестве отслеживаемой (`--set-upstream-to`).

```shell 
git config push.default simple
```
Выталкивать при `git push` в явно установленную отслеживаемую ветку, но только если имена удалённой и локальной веток совпадают.

```shell 
git config push.default current
```
Выталкивать `git push` в ветку с тем же именем, что и локальная ветка, даже если она не усктовлена как отслеживаемая.

```shell
git push origin HEAD
```

Если нет желания постоянно указывать имя текущей ветки при установленном режиме `current`


## Документация
[git config](https://mirrors.edge.kernel.org/pub/software/scm/git/docs/git-config.html)

[“simple” vs “current” push.default in git for decentralized workflow](https://stackoverflow.com/questions/23918062/simple-vs-current-push-default-in-git-for-decentralized-workflow)

[Why do I need to do `--set-upstream` all the time?](https://stackoverflow.com/questions/6089294/why-do-i-need-to-do-set-upstream-all-the-time)
