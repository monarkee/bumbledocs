# Configuring the Admin

The admin has a few options you can set in Bumble's config file.

## Site Title

This enables you to change the link text in the header of the admin

    'site-title' => 'Bumble CMS',

## Site URL

This lets you configure the URL a user is sent to when they click the "Visit Site" link in the header

    'site-url' => 'http://bumblecms.com',

## Authentication Columns

This lets you choose which columns to authenticate users with.

    'auth_columns' => ['email', 'password']

## Admin Prefix

This enables you to configure the prefix of the admin. If you wanted your admin to be located at `http://examplesite.com/system` you could set this value to:

    'admin_prefix' => 'system',

## Admin Routes

This lets you configure the URLs of the admin routes. This is useful if your app uses "Sign In" instead of "Login" or "Sign Out" instead of "Logout".

    'admin' => [
        'index' => 'index',
        'login' => 'login',
        'logout' => 'logout',
        'dashboard' => 'dashboard',
    ],