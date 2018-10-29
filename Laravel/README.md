# Laravel

## Install Laravel
```
composer create-project --prefer-dist laravel/laravel project-name
```

## See Site
```
php artisan serve
```

## Make Controller
```
//Route::get ...... @...
php artisan make:controller [PostController]

//Route::resource('photo','PhotoController')
php artisan make:controller --resource [PostController]
```

## Migration
```
php artisan migrate
```
* if you see this `Error 42000`, add this line to `app\Providers\AppServiceProvider.php`
```
use Illuminate\Support\Facades\Schema;
...
public function boot()
{
    Schema::defaultStringLength(191);
}
```

```
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
```
php artisan tinker
```

## Api
```
php artisan make:controller folderName/apiController --api
```

## route caching
```
php artisan route:cache
```

## add auth
```
php artisan make:auth
```

## Make Middleware
```
php artisan make:middleware RoleMiddleware
```

## down & restore the site
```
php artisan down
php artisan up
```

## Optimization for Deploy
```
//Autoloader
composer install --optimize-autoloader --no-dev

//Configuration Loading
php artisan config:cache

//Route Loading
php artisan route:cache
```