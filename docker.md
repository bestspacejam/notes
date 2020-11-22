# Docker

## Удаление всех повисших образов

Образы оставшиеся после сборки нового образа с именем которое уже использовалось до этого

```shell
docker images --quiet --filter="dangling=true" | xargs --no-run-if-empty docker rmi
docker image prune --force
```
