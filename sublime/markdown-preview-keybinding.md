# Просмотр скомпилированного Markdown-файла в браузере

Добавить запись в `Preferences/Key Binding`:

```json
{
	"keys": ["alt+m"],
	"command": "markdown_preview",
	"args": {"target": "browser", "parser":"markdown" },
	/* обрабатывать данное сочетание клавиш только в файлах Markdown  */
	"context": [
		{ "key": "selector", "operator": "equal", "operand": "text.html.markdown" }
	]
}
  
 ```