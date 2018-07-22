# Памятка по webpack-dev-server

## Обновление страницы при изменении скриптов и стилей

### `--inline` - window.location.reload()
Добавляет `['webpack-dev-server/client']` во все точки входа

[Ссылка на комментарий про --inline и --hot](https://github.com/webpack/webpack-dev-server/issues/97#issuecomment-69880395)

### `--hot` - веб-сокеты
- Добавляет плагин `new webpack.HotModuleReplacementPlugin()`
- Устанавливает опцию `{hot: true}`
- Добавляет скрипт `['webpack/hot/dev-server']` во все точки входа (если `{inlile: true}`)

[devServer.hot](https://webpack.js.org/configuration/dev-server/#devserver-hot) - документация
