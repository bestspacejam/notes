# Убрать надпись &quot;AppReady&quot; в webpack-dev-server

Запуск из коммандной строки:

```shell
webpack-dev-server --inline
```

Чтобы постоянно не писать флаг `--inline` можно настроить режим запуска в файле `webpack.config.js`:

```json
// Включение hot-reload для webpack-dev-server на http://localhost:8080/ без ToolBar-a
devServer: { inline: true }
```

После запуска в режиме &quot;inline&quot;, горячая перезагрузка без статусной строки будет доступна по адресу http://localhost:8080/

## Ссылки
[Документация Webpack v1](https://webpack.github.io/docs/webpack-dev-server.html#inline-mode)
