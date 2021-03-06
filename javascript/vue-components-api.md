# Заметка от API компонентов VUE

[Выдержка из документации](https://ru.vuejs.org/v2/guide/components.html#Создание-компонентов-для-повторного-использования):

> API компонентов Vue состоит из трёх частей: входных параметров, событий и слотов:
> 
> * **Входные параметры** позволяют передавать в компонент данные извне.
> * **События** позволяют компонентам воздействовать на внешнее окружение.
> * **Слоты** позволяют внешнему окружению дополнять компоненты новым контентом.


## Пользовательские события

```html
<input v-model="something">
```

Это сокращённая форма шаблона:

```html
<input v-bind:value="something" v-on:input="something = $event.target.value">
```