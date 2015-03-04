## Authentication

- [Overview](#overview)
- [Customizing a User's First and Last Name](#names)
- [Configuring Authentication Columns](#authcolumns)
- [Limiting Access To The Admin](#limitingaccess)

<a name="overview"></a>
## Overview
Laravel's authentication feature is supported out-of-the-box, and you may use your own ```User``` Eloquent model. To make it so Bumble can use your User model, simple add ```use BumbleUserTrait;``` to it. This allows the CMS to get the full name of the user and the [Gravatar](http://gravatar.com) for the user.

<a name="names"></a>
## Customizing a User's First and Last Name
By default, the admin will look for `first_name` and `last_name` columns and use those to show your name. If you wish to customize them, simply open the `bumble.php` configuration file and change the keys to the correct ones.

<a name="authcolumns"></a>
## Configuring Authentication Columns
Bumble allows you to configure the login to the admin. You will usually have a `User` model which authenticates with its `username` or `email` columns, along with a `password`. You can configure which columns are used in the `bumble.php` configuration file.

For example, you may want to set it up so your users log in with the same `email` and `password` they use in a different area of the app. You can set it up like this:

    'auth_columns' => ['email', 'password']

Bumble will then show the appropriate fields and will authenticate using that data.

<a name="limitingaccess"></a>
## Limiting Access To The Admin
Bumble checks that a user is authenticated before they can see the admin, but there are times when you only want certain users to be able to access the admin. To do that you simply have to reimpliment the `bumble_auth` filter in your app. Here's an example that checks if the first segment is Bumble's admin prefix setting and if the value of the user's group column is not equal to `0`.

    Route::filter('bumble_auth', function() {
        if (Request::segment(1) == config('bumble.admin_prefix') && Auth::user()->group != '0')
        {
            return Redirect::route('home');
        }
    });