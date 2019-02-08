# gvarghese/aws-rekognition

Forked from larareko/aws-rekognition and updated, as it was missing support for detectText support and appears to have been abandoned.

A Laravel package/facade for the Rekognition API PHP SDK.

This repository implements a simple Service Provider of the AWS Rekognition client, and makes it easily accessible via a Facade in Laravel >= 5. 

See [AWS Rekognition](https://aws.amazon.com/rekognition/) for more information.

## Requirements

Create an account at [AWS](https://aws.amazon.com/console/) and take note of your API keys.

## Installation using [Composer](https://getcomposer.org)

In your terminal application move to the root directory of your laravel project using the cd command and require the project as a dependency using composer.

composer require gvarghese/aws-rekognition

This will add the following lines to your composer.json and download the project and its dependencies to your projects ./vendor directory:

## Usage

With Laravel 5.5, the package should auto-register.

For older versions, open config/app.php and add the following lines ([a], [b]):

```php

// config/app.php

return [

    // ...

    'providers' => [

        // ...

        /*
         * Package Service Providers...
         */
        gvarghese\Rekognition\RekognitionServiceProvider::class, // [a]

        /*
         * Application Service Providers...
         */
        App\Providers\AppServiceProvider::class,
        App\Providers\AuthServiceProvider::class,
        App\Providers\EventServiceProvider::class,
        App\Providers\RouteServiceProvider::class,

    ],

    // ...

    'aliases' => [

        'App' => Illuminate\Support\Facades\App::class,
        'Artisan' => Illuminate\Support\Facades\Artisan::class,

        // ...

        'Rekognition' => 'gvarghese\Rekognition\RekognitionFacade', // [b]
        'Hash' => Illuminate\Support\Facades\Hash::class,

        // ...
    ],

];


```

## Publish Vendor

aws-rekognition requires a connection configuration. To get started, you'll need to publish all vendor assets running:

php artisan vendor:publish

This will create a config/rekognition.php file in your app that you can modify to set your configuration. Make sure you check for changes compared to the original config file after an upgrade.

Now you should be able to use the facade within your application. Ex:

```php

class LabelDetectionImage extends Model
{
    /**
     * Upload image to S3
     *
     * @param Illuminate\Http\UploadedFile  $file
     *
     * @return string
     */
    public function upload(UploadedFile $file) : string
    {
        $name = time() . $file->getClientOriginalName();
        
        \Rekognition::uploadImageToS3(file_get_contents($file), null, self::BUCKET, $name);
        
        return $name;
    }
}

```


## Contributing

Find an area you can help with and do it. Open source is about collaboration and open participation. 
Try to make your code look like what already exists or better and submit a pull request. Also, if
you have any ideas on how to make the code better or on improving the scope and functionality please
contact any of the contributors.

## License

MIT License.
