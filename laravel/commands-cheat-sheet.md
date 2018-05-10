# Команды фреймворка Laravel

`php artisan make:migration add_column_to_hosts_table --table="hosts"` - Создать миграцию для таблицы "hosts"
- `--table=tablename` - Изменение схемы указаной таблицы
- `--create=tablename` - Создание новой таблицы

`php artisan make:controller ControllerName --resource` - PhotoController --resource
-  `--resource` - создать [ресурсный контроллер](https://laravel.com/docs/5.5/controllers#resource-controllers)

`php artisan migrate --seed` - Запустить миграцию (`--seed` с заполнением данными)

`php artisan make:seeder UserTableSeeder` - Создать наполнитель базы данных

`php artisan migrate:reset` - Окатить все миграции

`php artisan db:seed --class=HostsTableSeeder` - Запустить указанного сидера

`php artisan make:model Host --migration` - Создать модель Host (`--migration` добавить миграцию)

`php artisan make:view index` - Создать вид

`php artisan make:provider HostProvider` - Создать класс сервис-провайдера

`php artisan cache:clear` - Сбросить кэш Laravel-а

`php artisan view:clear` - Удалить все скомпилированные view-файлы


## Дополнительные полезные команды

`composer dump-autoload` - Перегенерировать список загружаемых классов
