# Getting started

Our [Laravel 5](http://laravel.com) package is created and is maintained by the [MainpixelV4](https://www.mainpixel.io) team. This package make it possible to interact with version 4 or above with your [Laravel 5](http://laravel.com) framework. Feel free to check out the [change log](laravel_changelog).

## Requirements

[PHP](https://php.net) 7+    
[Laravel](https://laravel.com) 5.2+

## Install Laravel package

To get the latest version of the Laravel Mainpixel package, simply require the project using [composer](https://getcomposer.org).

```bash
$ composer require mainpixelbv/laravel-mainpixel
```

Instead, you may of course manually update your require block and run `composer update` if you so choose:

```json
{
    "require": {
        "mainpixelbv/laravel-mainpixel": "^1.0"
    }
}
```

Once Laravel Mainpixel is installed, you need to register the service provider. Open up `config/app.php` and add the following to the `providers` key.

`'mainpixelbv\laravel-mainpixel\MainpixelApiServiceProvider'`

## Configuration

Laravel Mainpixel requires connection configuration.

To get started, you'll need to publish all vendor assets:

```bash
$ php artisan vendor:publish
```

This will create a `config/MainpixelApi.php` file in your app that you can modify to set your configuration. Also, make sure you check for changes to the original config file in this package between releases.

## Usage
Add a `namespace` by choosing the right type, like `Containers`, `Databases`, `Contacts`

```php
use Mainpixel\Api\Types\Hosting\{type};
```
