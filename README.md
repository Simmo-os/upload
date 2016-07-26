## Ajax Upload for Laravel 5

[![Latest Stable Version](https://poser.pugx.org/recca0120/upload/v/stable)](https://packagist.org/packages/recca0120/upload)
[![Total Downloads](https://poser.pugx.org/recca0120/upload/downloads)](https://packagist.org/packages/recca0120/upload)
[![Latest Unstable Version](https://poser.pugx.org/recca0120/upload/v/unstable)](https://packagist.org/packages/recca0120/upload)
[![License](https://poser.pugx.org/recca0120/upload/license)](https://packagist.org/packages/recca0120/upload)
[![Monthly Downloads](https://poser.pugx.org/recca0120/upload/d/monthly)](https://packagist.org/packages/recca0120/upload)
[![Daily Downloads](https://poser.pugx.org/recca0120/upload/d/daily)](https://packagist.org/packages/recca0120/upload)

## Features
- Support [Plupload](http://www.plupload.com/) Chunks
- Support [FileApi](http://mailru.github.io/FileAPI/) Chunks

## Installing

To get the latest version of Laravel Exceptions, simply require the project using [Composer](https://getcomposer.org):

```bash
composer require recca0120/upload
```

Instead, you may of course manually update your require block and run `composer update` if you so choose:

```json
{
    "require": {
        "recca0120/upload": "^1.2.0"
    }
}
```

Include the service provider within `config/app.php`. The service povider is needed for the generator artisan command.

```php
'providers' => [
    ...
    Recca0120\Upload\ServiceProvider::class,
    ...
];
```

## How to use

Controller
```php

use Recca0120\Upload\Manager;
use Symfony\Component\HttpFoundation\File\UploadedFile;

class UploadController extends Controller
{
    public function upload(Manager $manager)
    {
        $driver = 'plupload'; // or 'fileapi'
        $name = 'file'; // $_FILES index;
        return $manager
            ->driver($driver)
            ->receive($name, function (UploadedFile $file) {

                $clientOriginalName = $file->getClientOriginalName();
                $pathName = $file->getPathname();
                $mimeType = $file->getMimeType();
                $size = $file->getSize();

                return response()->json([
                    'name'     => $clientOriginalName,
                    'type'     => $mimeType,
                    'size'     => $size,
                ]);
            });
    }
}
```
