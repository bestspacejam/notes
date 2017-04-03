# Работа с PIP


Сохранение списка пакетов в файл requirements.txt:

```shell
pip freeze > requirements.txt
```

Загрузка всех пакетов перечисленных в файле requirements.txt:

```shell
pip install -r /path/to/requirements.txt
```

## Ссылки
[Мануал по pip freeze](https://pip.pypa.io/en/stable/reference/pip_freeze/)