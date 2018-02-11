# Мульти-аутентификация в Laravel

1. Скопировать контроллеры из пространства имён `App\HttpControllers\Auth` в `App\HttpControllers\Admin`
2. Скопировать представления из `resources/views/auth/` в `resources/views/admin/`
    - Скопировать `resources/views/home.blade.php` в `resources/views/admin/home.blade.php`
3. Скопировать роуты из Auth::routes в "admin"
    - Переименовать Auth в Admin
4. Скопировать HomeController в AdminController
    - Закоментировать `$this->middleware('auth');`
5. В файле `config/auth.php`
    - в опции `guards` скопировать `web` в новый ключ `admin`, прописать в значениях `'provider' => 'admins'`:
        ```php
        'guards' => [
            'web' => [
                'driver' => 'session',
                'provider' => 'users',
            ],

            'admin' => [
                'driver' => 'session',
                'provider' => 'admins',
            ],

            'api' => [
                'driver' => 'token',
                'provider' => 'users',
            ],
        ]
        ```
    - В опции `providers` скопировать `users` в `admins` прописав класс `model => App\Admin`:
        ```php
        'providers' => [
            'users' => [
                'driver' => 'eloquent',
                'model' => App\User::class,
            ],

            'admins' => [
                'driver' => 'eloquent',
                'model' => App\Admin::class,
            ],
        ],
        ```
    - В опции `passwords` скопировать `users` в `admins` прописав `provider => 'admins'`:
        ```php
        'passwords' => [
            'users' => [
                'provider' => 'users',
                'table' => 'password_resets',
                'expire' => 60,
            ],
            'admins' => [
                'provider' => 'admins',
                'table' => 'password_resets',
                'expire' => 60,
            ],
        ],
        ```
6. Скопирвать класс модели из User в Admin
7. В классе Admin/LoginController
    - Отредактировать параметр `redirectTo`
    - Изменить middleware на "guest:admin":
    
        ```php
        class LoginController extends Controller
        {
            use AuthenticatesUsers;
            protected $redirectTo = '/admin';
            
            public function __construct()
            {
                $this->middleware('guest:admin')->except('logout');
            }

            public function username()
            {
                return 'username';
            }
        }
        ```
    
8. В классе Admin/PasswordController
    - Изменить middleware на "guest:admin"
9. В классе Admin/RegisterController
    - Отредактировать параметр `redirectTo`
    - Изменить middleware на "guest:admin"
10. В классе Admin/PasswordResetController
    - Отредактировать параметр `redirectTo`
    - Изменить middleware на "guest:admin"
11. Создать миграцию для таблицы `admins`:
    ```shell
    php artisan make:migration create_admins_table --create admins
    ```
    
    - Добавить поднятие миграции: 
        ```php
        public function up()
        {
            Schema::create('admins', function (Blueprint $table) {
                $table->increments('id');
                $table->string('username')->unique();
                $table->string('password');
                $table->string('email');
                $table->rememberToken();
                $table->timestamps();
            });
        }
        ```
    