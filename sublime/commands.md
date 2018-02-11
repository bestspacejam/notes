# Полезные команды Sublime Text 3

## Посмотреть имя текущей области текста

Ctrl+`
```
print(view.scope_name(view.sel()[0].b))
```