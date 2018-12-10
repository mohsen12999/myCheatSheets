# Laravel

## Install Laravel

```sh
composer create-project --prefer-dist laravel/laravel project-name
```

## See Site

* for not use xampp or docker

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

## Docker

[simple-approach-using-docker-with-php](https://bitpress.io/simple-approach-using-docker-with-php/)
[laravel-docker-part-1-setup-for-development](https://medium.com/@shakyShane/laravel-docker-part-1-setup-for-development-e3daaefaf3c)
[laradock](https://laradock.io/)
[laradock](https://github.com/laradock/laradock)
[laravel-in-docker](https://buddy.works/guides/laravel-in-docker)

* make files

`mkdir .docker/`
`touch .docker/Dockerfile .docker/vhost.conf`
`touch docker-compose.yml`

```Dockerfile
FROM php:7.1.8-apache

MAINTAINER Paul Redmond

COPY . /srv/app
COPY .docker/vhost.conf /etc/apache2/sites-available/000-default.conf

RUN chown -R www-data:www-data /srv/app \
    && a2enmod rewrite
```

* vhost.conf

```conf
<VirtualHost *:80>
    DocumentRoot /srv/app/public

    <Directory "/srv/app/public">
        AllowOverride all
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

* Building the Image

`docker build --file .docker/Dockerfile -t laravel-docker .`

* docker-compose.yml

```yml
version: '3'
services:
  app:
    build:
      context: .
      dockerfile: .docker/Dockerfile
    image: laravel-docker
    ports:
      - 8080:80
```

## Deploy

* change php ver to 7.2 in cpanel

```sh
#!/bin/bash

mkdir ../${PWD##*/}_deploy
mkdir ../${PWD##*/}_deploy/index
cp -rf ./* ../${PWD##*/}_deploy/index
cp -rf ./public/* ../${PWD##*/}_deploy/

# can run optimize method

rm -rf ../${PWD##*/}_deploy/index/public
rm -rf ../${PWD##*/}_deploy/index/.docker
rm -rf ../${PWD##*/}_deploy/index/deploy.sh
rm -rf ../${PWD##*/}_deploy/index/readme.md

sed -i 's/\.\./index/g' ../${PWD##*/}_deploy/index.php

echo copy .env to index folder

#compress
```