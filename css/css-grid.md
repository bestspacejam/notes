# CSS Grid
Параметры `auto-fill` и `auto-fit` ведут себя одинаково, если ширины элементов в гриде достаточно для его заполнения.
Если общей ширины недостаточно, `auto-fill` - сжимает треки до минимального размера, а `auto-fit` - растягивает треки до максимальной ширины.

Примеры и описание:
- [auto-fill vs. auto-fit](https://gridbyexample.com/examples/example37/)
- [Auto-Sizing Columns in CSS Grid: `auto-fill` vs `auto-fit`](https://css-tricks.com/auto-sizing-columns-css-grid-auto-fill-vs-auto-fit/)
- [Repeat-to-fill: auto-fill and auto-fit repetitions](https://drafts.csswg.org/css-grid/#auto-repeat) (описание из CSS стандарта)


## Выравнивание

- `{justify,align}-items` - выравнивает содержимое ячеек по горизонтали и по вертикали (start | end | center | stretch)
- `{justify,align}-content` - выравнивает содержимое grid-контейнера (start | end | center | stretch | space-around | space-between | space-evenly)
