# Reliese Laravel

[![StyleCI](https://styleci.io/repos/71080508/shield?style=flat)](https://styleci.io/repos/71080508)
[![Build Status](https://travis-ci.org/haakco/reliese-laravel-models.svg?branch=master)](https://travis-ci.org/haakco/reliese-laravel-models)
[![Latest Stable Version](https://poser.pugx.org/haakco/reliese-laravel-models/v/stable)](https://packagist.org/packages/haakco/reliese-laravel-models)
[![Total Downloads](https://poser.pugx.org/haakco/reliese-laravel-models/downloads)](https://packagist.org/packages/haakco/reliese-laravel-models)
[![Latest Unstable Version](https://poser.pugx.org/haakco/reliese-laravel-models/v/unstable)](https://packagist.org/packages/haakco/reliese-laravel-models)
[![License](https://poser.pugx.org/haakco/reliese-laravel-models/license)](https://packagist.org/packages/haakco/reliese-laravel-models)

This is a clone of Reliese Laravel with some submitted patches applied.

Most importantly the ones that add support for postgres.
 
As they don't seem to be actively maintaining this I've forked and applied the patches.

If they start actively maintaining the project and merging patches I'll remove this one as would prefer the get the 
acknowledgment for their hard work. 

Reliese Laravel is a collection of Laravel Components which aim is 
to help the development process of Laravel applications by 
providing some convenient code-generation capabilities.

## How does it work?

This package expects that you are using Laravel 5.1 or above.
You will need to import the `haakco/reliese-laravel-models` package via composer:

```shell
composer require haakco/reliese-laravel-models
```

### Configuration

Add the service provider to your `config/app.php` file within the `providers` key:

```php
// ...
'providers' => [
    /*
     * Package Service Providers...
     */

    Reliese\Coders\CodersServiceProvider::class,
],
// ...
```
### Configuration for local environment only

If you wish to enable generators only for your local environment, you should install it via composer using the --dev option like this:

```shell
composer require haakco/reliese-laravel-models --dev
```

Then you'll need to register the provider in `app/Providers/AppServiceProvider.php` file.

```php
public function register()
{
    if ($this->app->environment() == 'local') {
        $this->app->register(\Reliese\Coders\CodersServiceProvider::class);
    }
}
```

## Models

![Generating models with artisan](https://cdn-images-1.medium.com/max/800/1*hOa2QxORE2zyO_-ZqJ40sA.png "Making artisan code my Eloquent models")

Add the `models.php` configuration file to your `config` directory and clear the config cache:

```shell
php artisan vendor:publish --tag=reliese-models
php artisan config:clear
```

### Usage

Assuming you have already configured your database, you are now all set to go.

- Let's scaffold some of your models from your default connection.

```shell
php artisan code:models
```

- You can scaffold a specific table like this:

```shell
php artisan code:models --table=users
```

- You can also specify the connection:

```shell
php artisan code:models --connection=mysql
```

- If you are using a MySQL database, you can specify which schema you want to scaffold:

```shell
php artisan code:models --schema=shop
```

### Customizing Model Scaffolding

To change the scaffolding behaviour you can make `config/models.php` configuration file
fit your database needs. [Check it out](https://github.com/haakco/reliese-laravel-models/blob/master/config/models.php) ;-)

### Tips

#### 1. Keeping model changes

You may want to generate your models as often as you change your database. In order
not to lose you own model changes, you should set `base_files` to `true` in your `config/models.php`.

When you enable this feature your models will inherit their base configurations from
base models. You should avoid adding code to your base models, since you
will lose all changes when they are generated again.

> Note: You will end up with two models for the same table and you may think it is a horrible idea 
to have two classes for the same thing. However, it is up to you
to decide whether this approach gives value to your project :-)

#### Support

For the time being, this package only supports MySQL databases. Support for other databases will be added soon.
