# Sed

### Вывод нескольких первых строк

```shell
sed 7q
```

### Вывод первой и последней строки

```shell
sed '1b;$!d'
sed -n '1p;n;$p'
```


### Удаление BOM

```shell
sed '1s/^\xEF\xBB\xBF//'
```


### Объединение мягких переносов строк

```shell
sed ':x; /=$/{N;bx}; s/=\n//g' <<'EOL'
All the wor=
ld's a stag=
e,
And all the=
 men and wo=
men merely =
players:
They have t=
heir exits =
and their e=
ntrances;
And one man=
 in his tim=
e plays man=
y parts.
EOL
```

### Создание списка из абcолютного пути и имени файла

```shell
sed -E 's/^(\/([^\/]+))+$/\0\t\2/'
```

### Создание таблицы из чередующихся строк 

```
$ seq 10 | sed -En 'h;n;G;y/\n/\t/;p'
2       1
4       3
6       5
8       7
10      9
```

### Удаление конечных символов `\r` из файла

```shell
sed -i 's/\r$//' filename
```

### Видео
- [Understanding how sed works 1/4](https://www.youtube.com/watch?v=l0mKlIswojA)
- [Understanding how sed works 2/4](https://www.youtube.com/watch?v=4vr8Aao0Mfo)
- [Understanding how sed works 3/4](https://www.youtube.com/watch?v=P4ZcBrJ38I8)
- [Understanding how sed works 4/4](https://www.youtube.com/watch?v=W95wrzAgdWk)

