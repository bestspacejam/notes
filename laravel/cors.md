# Подключение CORS в Laravel 5.5

## Библиотека

[barryvdh/laravel-cors](https://github.com/barryvdh/laravel-cors)

## Установка
```
composer require barryvdh/laravel-cors
```
## Настройка

Копирование конфигурации:
```shell
php artisan vendor:publish --provider="Barryvdh\Cors\ServiceProvider"
```

В результате в файле `config/cors.php` должно появится:
```php
return [
    'supportsCredentials' => false,
    'allowedOrigins' => ['*'],
    'allowedHeaders' => ['Content-Type', 'X-Requested-With'],
    'allowedMethods' => ['*'], // ex: ['GET', 'POST', 'PUT',  'DELETE']
    'exposedHeaders' => [],
    'maxAge' => 0,
]
```

Прописать middleware в файл `app/Http/Kernel.php`:
```php
protected $middlewareGroups = [
    'web' => [
       // ...
    ],

    'api' => [
        // ...
        \Barryvdh\Cors\HandleCors::class,
    ],
];
```
