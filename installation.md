# Installation

Bumble is installed via Composer. To get started, simply add the following to your ````composer.json```` file:

"monarkee/bumble": "dev-master"

Once you run ```composer update```, you can publish the config file and public assets to their proper places by running a couple of Artisan commands:

php artisan asset:publish

php artisan config:publish monarkee/bumble

The next step is to add Bumble's Service Provider to your ```app.php``` file in the ```config``` folder. In the ```providers``` array, simply add this:

'Monarkee\Bumble\BumbleServiceProvider',

## Jumpstarting Your Users Table

You can allow Bumble to generate your users table and populate it with a test admin user by issuing the following commands:

    php artisan migrate --package=monarkee/bumble
    php artisan db:seed --class=BumbleSeeder

This command runs the migrations for the bumble package and seeds the database with an admin user. The admin user is `admin`, its email is `admin@bumble.dev`, and the password is `password`. It's recommended that you change this to whatever data you'd like upon first install.
