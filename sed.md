# Sed

## Основные моменты

```
-e, -n, -f
диапазоны, {}
p/d
;
=/n
P/D/N
q
#
s///Iwp
y///
r,w
l
a/i/c
x/h/H/g/G
:/b/t
```

## Использование

```shell
# Вывести первую и последнюю строку
sed '1b;$!d'
sed -n '1p;n;$p'

# Вывести первые семь строк
sed 7q

# Удалить BOM
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
