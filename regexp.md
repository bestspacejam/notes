# Регулярные выражения

## Lookahead Hacks

Пароль минимум из 6 символов
(одно число, одна буква и один символ): 

```
/^(?=.*\d)(?=.*[a-z])(?=.*[\W_]).{6,}$/i
```

Любое число не делящееся на 50: 
```
/\b(?!\d+[50]0)\d+\b/
```

Всё, что не содержит foo:
```
/^(?!.*foo).+$/
```



## Ссылки

[Best of Fluent 2012: /Reg(exp){2}lained/: Demystifying Regular Expressions](https://www.youtube.com/watch?v=EkluES9Rvak) - видео с конференции
