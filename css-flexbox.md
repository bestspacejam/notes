# Заметки о Flexbox

- `flex-grow` &mdash; сколько частей незанятого в родительском блоке пространства можно добавить к блоку
- `flex-shrink` &mdash; сколько частей переполнения родительского блока можно убрать из блока
- `flex-basis` &mdash; базовая ширина для блока, аналог свойства `width`

## `flex-grow`
Считается количество **&quot;grow&quot;** во всём контейнере, делится на ширину свободного пространства и добавляется к блоку согласно указанному в нём значению `flex-grow`.

## `flex-shrink`
Аналогично действует **&quot;shrink&quot;** &mdash; считается количество `flex-shrink` в контейнере, делится на ширину переполнения и вычитается из каждого блока согласно значению `flex-shrink` 

## `flex-basis`
Имеет приоритет перед свойством `width` во *flex*-контейнере, при этом действует аналогично &mdash; изменяет базовую ширину блока.

При указании `flex-basis:auto` ширина блока откатывается к значению свойства `width`.

Базовая ширина блока установится в 30 пикселей:
```css
div {
	flex-basis: auto;
	width: 30px;
}
```

Если указать `flex-basis:0`, то элементы распределяются пропорционально (как *fractional unit* в Grid), ширина/высота блока расчитается исходя из всего пространства fLexbox-контейнера, без учёта размера содержимого самого блока.

Необходимо учитывать, что блок не может быть меньше чем задано свойствами `min-width`/`min-height`, которые по-умолчанию имеют значение `auto` и будут растягивать его если содержимое не помещается в контейнер.

Если `flex-basis` равен `auto`, то для расчёта ширины/высоты элемента берётся значение из `width`/`height` если там оно тоже `auto` то `flex-basis` принимает значение `content`.

### `flex-basis` ограничено свойствами `min-width` / `max-width`

Свойства `min-width` и `max-width` имеют приоритет перед `flex-basis` и ораничивают его.

```css
div {
	flex-basis: 500px;
	max-width: 100px;
}
```

В этом примере, свойство `max-width` ограничивает базовую ширину блока 100 пикселями.


## Ссылки

- [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [11 things I learned reading the flexbox spec](https://hackernoon.com/11-things-i-learned-reading-the-flexbox-spec-5f0c799c776b)
- [`flex-grow` is weird. Or is it?](https://css-tricks.com/flex-grow-is-weird/)
- [flex-shrink](https://css-tricks.com/almanac/properties/f/flex-shrink/)
- [The Difference Between Width and Flex Basis](http://gedd.ski/post/the-difference-between-width-and-flex-basis/)
