## Installation

Bumble is installed via Composer. To get started, simply add the following to your ````composer.json```` file:

"monarkee/bumble": "dev-master"

Once you run ```composer update```, you can publish the config file and public assets to their proper places by running a couple of Artisan commands:

php artisan asset:publish

php artisan config:publish monarkee/bumble

The next step is to add Bumble's Service Provider to your ```app.php``` file in the ```config``` folder. In the ```providers``` array, simply add this:

'Monarkee\Bumble\BumbleServiceProvider',


