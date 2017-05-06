# Порядок обработки исключений

## Пример
```python
def error_test():
	try:
		print("try")
		raise NameError("NameError")
		return "try's return"
	except NameError as e:
		print("catched <{}>".format(e))
		return "except's return"
	else:
		print("else")
		return "else's return"
	finally:
		print("finnaly")
		return "finally's return"

print("RESULT: {}".format(error_test()))
```

Результат выполнения:

```
try
catched <NameError>
finnaly
RESULT: except's return
```


## Try
- Если в блоке "**try**" указан возврат значения или выход из цикла - блок "**else**" не выполняется

## Else
- Блок "**else**" выполняется только если блок "**try**" не вызвал исключение, не выполнил возврат значения не выпонил выход из цикла (*break*) или продолжение цикла (*continue*)

## Finally
- Блок "**finally**" выполняется всегда, и всегда последним
- Если в блоке "**finally**" указан возврат значения - оно имеет приоритет перед значениями возвращаемыми другими блоками (*try*, *except*, *else*)
- Если в блоке "**finally**" нет возврата значения, то используется значение выполненного блока, то есть если поймано исключение то блока "except"