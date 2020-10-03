# Установка простейшего сервера статических файлов для node.js

```shell
npm install serve-static --save-dev
npm install connect --save-dev

```

Файл `package.json`:

```
"scripts": {
    "server": "node server.js",
}
```

Файл `server.js`

```javascript
const connect = require('connect');
const serveStatic = require('serve-static');
const path = require("path");

// Директория с файлами
const folder = ".";

// Порт сервера
const port = 8888;

const document_root = path.join(__dirname, folder);

connect().use(serveStatic(document_root, { dotfiles: "ignore" })).listen(port, function(){
	console.log(`Server running on http://localhost:${port}`);
});
```