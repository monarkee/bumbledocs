## Authentication

Laravel's authentication feature is supported out-of-the-box, and you may use your own ```User``` Eloquent model. To make it so Bumble can use your User model, simple add ```use BumbleUserTrait;``` to it. This allows the CMS to get the full name of the user and the [Gravatar](http://gravatar.com) for the user.

## Bumble's Log In

Bumble allows you to configure the login to the admin. You will usually have a `User` model which has a mix of columns commonly used for authentication: `username` and `password`, or `email` and `password`. You can configure this in the packages config file.

For example, you may want to set it up so your users log in with the same `email` and `password` they use in a different area of the app. You can set it up like this:

    'auth_columns' => ['email', 'password']

Bumble will know how to show the appropriate fields and authenticate using that data.

## Limiting Access To Certain Users

Bumble checks that a user is authenticated before they can see the admin, but there are times when you only want certain users to be able to access the admin. To do that you simply have to reimpliment the `bumble_auth` filter in your app. Here's an example that checks if the first segment is Bumble's admin prefix setting and if the value of the user's group column is equal to `0`.

    Route::filter('bumble_auth', function() {
        if (Request::segment(1) == Config::get('bumble::admin_prefix') && Auth::user()->group != '0')
        {
            return Redirect::route('home');
        }
    });