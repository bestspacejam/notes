# Контроллеры Laravel

## Правила наименования для связи роутов и действий

|Verb|URI|Action|Route Name|
|--- |--- |--- |--- |
|GET|/photos|index|photos.index|
|GET|/photos/create|create|photos.create|
|POST|/photos|store|photos.store|
|GET|/photos/{photo}|show|photos.show|
|GET|/photos/{photo}/edit|edit|photos.edit|
|PUT/PATCH|/photos/{photo}|update|photos.update|
|DELETE|/photos/{photo}|destroy|photos.destroy|

Взято из раздела документации: [Resource Controllers](https://laravel.com/docs/5.5/controllers#resource-controllers)
