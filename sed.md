# Sed

## Вывод нескольких первых строк

```shell
sed 7q
```

## Вывод первой и последней строки

```shell
# 
sed '1b;$!d'
sed -n '1p;n;$p'
```


## Удаление BOM

```shell
sed '1s/^\xEF\xBB\xBF//'
```


## Объединение мягких переносов строк

```shell
sed ':x; /=$/{N;bx}; s/=\n//g' jaques.txt
```

### jaques.txt
```
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
```
