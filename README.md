# HubSpot PHP API Client Wrapper for Laravel
This is a wrapper for the [ryanwinchester/hubspot-php](https://github.com/ryanwinchester/hubspot-php) package and gives the user a Service Container binding and facade of the `SevenShores\Hubspot\Factory::create('api-key')` function.

## Installation
1. `composer require rossjcooper/laravel-hubspot`
2. Get a HubSpot API Key from the Intergrations page of your HubSpot account.
3. Laravel 5.4 or earlier, in your `config/app.php` file:
    - Add `Rossjcooper\LaravelHubSpot\HubSpotServiceProvider::class` to your providers array.
    - Add `'HubSpot' => Rossjcooper\LaravelHubSpot\Facades\HubSpot::class` to your aliases array.
4. `php artisan vendor:publish --provider="Rossjcooper\LaravelHubSpot\HubSpotServiceProvider" --tag="config"` will create a `config/hubspot.php` file.
5. Add your HubSpot API key into the your `.env` file: `HUBSPOT_API_KEY=yourApiKey`

## Usage
You can use either the facade or inject the HubSpot class as a dependency:
### Facade
```php
// Echo all contacts first and last names
$response = HubSpot::contacts()->all();
    foreach ($response->contacts as $contact) {
        echo sprintf(
            "Contact name is %s %s." . PHP_EOL,
            $contact->properties->firstname->value,
            $contact->properties->lastname->value
        );
    }
```
### Dependency Injection
```php
Route::get('/', function (Rossjcooper\LaravelHubSpot\HubSpot $hubspot) {
    $response = $hubspot->contacts()->all();
    foreach ($response->contacts as $contact) {
        echo sprintf(
            "Contact name is %s %s." . PHP_EOL,
            $contact->properties->firstname->value,
            $contact->properties->lastname->value
        );
    }
});
```

For more info on using the actual API see the main repo [ryanwinchester/hubspot-php](https://github.com/ryanwinchester/hubspot-php)

## Issues
Please only report issues relating to the Laravel side of things here, main API issues should be reported [here](https://github.com/ryanwinchester/hubspot-php/issues)
