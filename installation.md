# Installation

## Composer

Bumble is installed via Composer. To get started, simply add the following to your `composer.json` file, and run `composer update`:

    "monarkee/bumble": "dev-master"

## Registering the Service Provider

The next step is to add Bumble's Service Provider to your `app.php` file in the `config` folder. In the `providers` array, simply add this:

    'Monarkee\Bumble\Providers\BumbleServiceProvider'

## Publishing Assets & Configuration

After that, you can publish the configuration file and public assets to their proper places by running a couple of Artisan commands:

    php artisan vendor:publish --provider="Monarkee\Bumble\Providers\BumbleServiceProvider" --tag="config"

    php artisan vendor:publish --provider="Monarkee\Bumble\Providers\BumbleServiceProvider" --tag="assets"

## Jumpstarting Your Users Table

Bumble can generate a users table and populate it with a test admin user by publishing its migrations into your app and issuing the following commands:

    php artisan vendor:publish --provider="Monarkee\Bumble\Providers\BumbleServiceProvider" --tag="migrations"

    composer update

    php artisan migrate

    php artisan db:seed --class=BumbleSeeder

This command publishes the migrations for a `Users` and seeds the database with an admin user. The admin's username is `admin`, its email is `admin@bumble.dev`, and the password is `password`. It's recommended that you change this to whatever data you'd like upon your first login to the admin.

> Note: you can set which columns to authenticate by setting the `auth_columns` array inside of `config/bumble.php`.
