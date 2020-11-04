# AWK

## Сравнение файлов

```shell
awk '
  NR == FNR {
    arr[$0]
    next
  }

  $0 in arr {
    print $0, "in both files"
  }
' c1.txt c2.txt
```

### c1.txt
```
aaa
bbb
ccc
```

### c2.txt
```
111
222
aaa
```
