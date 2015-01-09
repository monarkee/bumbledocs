# Custom Views

You may want to have specialized views in your Bumble installation for things like dashboards, news updates, etc. This is really easy to accomplish! Here's an outline of how to do that:

1. Create a route
2. Create your custom Bumble Controller
3. Extend the Bumble Layout
4. Rejoice

### 1. Create a route

You can create a route that uses the admin prefix you've set for your installation by calling `Config::get('bumble::admin_prefix')`. If you ever change the admin prefix, this will make sure your route changes as well.

    Route::get(Config::get('bumble::admin_prefix').'/coolio', [
        'uses' => 'CustomController@index',
    ]);

### 2. Create a controller

Your controller can do anything a normal one would, so feel free to go crazy. Here were are simply going to show a custom widget in the view, but you could pull from your Models, an API, or anything!

    <?php

    class CustomController extends BaseController
    {
        public function index()
        {
            return View::make('custom.index');
        }
    }

### 3. Extend The Bumble Layout

Your custom view can share Bumble's master layout by extending it in your view like so:

    @extends('bumble::layouts.master')

    @section('content')
        <section class="main-area">
            <main class="main-content">
                <div class="header">
                    <div class="flex jcc aic acc">
                        <h2 class="header__title">Statistics</h2>
                    </div>
                </div>

                {{!-- Your content goes here --}}
            </main>
        </section>
    @stop

For extra credit, use the CSS class names from Bumble's installation.