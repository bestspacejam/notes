Создание пароля

```php
$user = new \App\User;
$user->password = Hash::make('password');
```

API token authenticaion

```php
$user->api_token = str_random(60);
```
