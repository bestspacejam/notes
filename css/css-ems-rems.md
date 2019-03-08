# Единицы &laquo;em&raquo; и &laquo;rem&raquo; в размерах шрифтов и отступах CSS

**EM** &mdash; Масштабируется относительно родительского элемента.
**REM** &mdash; Масштабируется относительно корневого элемента (т.е. `body`).

Пример:

```css
body { font-size: 30px; }
div.container { font-size: 10px; }

/* font-size установится в 20px */
div.container > p { font-size: 2em; }

/* font-size установится в 15px  */
div.container > h1 { font-size: 0.5rem; }
```

## EM / REM в @media
Единицы &quot;em&quot; и &quot;rem&quot; в медиа-запросах масштабируются относительно пользовательского размера шрифта. То есть если указать `body { font-size: 30px; }` ограничение заданное в &quot;em&quot; будет опираться на значение установленное в браузере пользователя (по умолчанию это 16px).

Пример:

```html
<!DOCTYPE html>
<style type="text/css">
body { font-size: 30px; }

h1 {
	padding: 1em;
	font-size: 1em;
	background: green;
	color: #fff;
}

/* 767px / 16px = 47.9375em */
@media only screen and (max-width: 47.9375em)
{
	h1 { background: red; }
}
</style>

<h1>test text block</h1>
```

Статья о размерах шрифтов в &laquo;em&raquo; и пикселях: [R.I.P. REM, Viva CSS Reference Pixel!](https://mindtheshift.wordpress.com/2015/04/02/r-i-p-rem-viva-css-reference-pixel/)