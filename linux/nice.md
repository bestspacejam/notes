# Nice & Priority - Приоритет выполняемых процессов
```shell
# Запустить процесс со значением nice (10 по умолчанию)
nice [command]

# Запустить процесс со значением nice равным 2
nice -n 2 [command]

# Изменить значение nice на 2 для запущенного процесса
renice -n 2 -p [pid]

# Изменить значение nice на 2 для всех процессов пользователя
renice -n 2 -u [user]
```
### Ссылки
- [Linux Nice and Priority values](https://www.youtube.com/watch?v=II2M3rqgCQA)
