Лог выполняемых запросов
```php
DB::enableQueryLog();
DB::table('users')->where('name', 'John')->first();
DB::getQueryLog();
```
