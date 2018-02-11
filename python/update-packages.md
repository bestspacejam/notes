# Pyhon - Обновление пакетов

```shell
pip freeze -- local | grep -v '^\-e' | cut -d = -f 1 | xargs -n 1 pip install -U
```

[источник](https://stackoverflow.com/questions/2720014/upgrading-all-packages-with-pip)