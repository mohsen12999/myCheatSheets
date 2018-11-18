# Laravel

## Install Laravel

```sh
composer create-project --prefer-dist laravel/laravel project-name
```

## See Site

```sh
php artisan serve
```

## Make Controller

```sh
//Route::get ...... @...
php artisan make:controller [PostController]

//Route::resource('photo','PhotoController')
php artisan make:controller --resource [PostController]
```

## Migration

```sh
php artisan migrate
```

* if you see this `Error 42000`, add this line to `app\Providers\AppServiceProvider.php`

```php
use Illuminate\Support\Facades\Schema;
...
public function boot()
{
    Schema::defaultStringLength(191);
}
```

```sh
//Best one Make Model and Table
php artisan make:model Flight --migration

php artisan make:migration create_users_table --create=users
php artisan make:migration add_votes_to_users_table --table=users


php artisan migrate:rollback
php artisan migrate:rollback --step=5
php artisan migrate:reset
php artisan migrate:refresh
php artisan migrate:refresh --seed => with seed
php artisan migrate:refresh --step=5

php artisan migrate:fresh
php artisan migrate:fresh --seed
```

## shell

```sh
php artisan tinker
```

## Api

```sh
php artisan make:controller folderName/apiController --api
```

## route caching

```sh
php artisan route:cache
```

## add auth

```sh
php artisan make:auth
```

## Make Middleware

```sh
php artisan make:middleware RoleMiddleware
```

## down & restore the site

```sh
php artisan down
php artisan up
```

## Optimization for Deploy

```sh
//Autoloader
composer install --optimize-autoloader --no-dev

//Configuration Loading
php artisan config:cache

//Route Loading
php artisan route:cache
```