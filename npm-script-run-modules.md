
# Модули для запуска скриптов

**[shx](https://www.npmjs.com/package/shx)** - Portable Shell Commands for Node
**[cross-env](https://www.npmjs.com/package/cross-env)** - Run commands that set environment variables across platforms
**[npm-run-all](https://www.npmjs.com/package/npm-run-all)** - A CLI tool to run multiple npm-scripts in parallel or sequential.
**[nodemon](https://www.npmjs.com/package/nodemon)** - Следит за файлами и перезапускает приложение при их изменении


Пример конфигурационного файла `package.json` для запуска скрипта Express сервера:


```json
{
  "name": "ssr-simple",
  "version": "1.0.0",
  "scripts": {
    "cp:dev": "shx cp node_modules/vue/dist/vue.js assets/vue.js",
    "cp:prod": "shx cp node_modules/vue/dist/vue.min.js assets/vue.js",
    "serve": "cross-env VUE_ENV=server nodemon --watch . --ext js,html server.js",
    "dev": "npm-run-all cp:dev serve",
    "prod": "npm-run-all cp:prod serve"
  },
  "author": "Chris Fritz",
  "license": "MIT",
  "dependencies": {
    "express": "^4.14.0",
    "vue": "^2.0.0-rc.3",
    "vue-server-renderer": "^2.0.0-rc.3"
  },
  "devDependencies": {
    "nodemon": "^1.10.2",
    "npm-run-all": "^3.0.0",
    "cross-env": "^3.1.3",
    "shx": "^0.1.4"
  }
}
```