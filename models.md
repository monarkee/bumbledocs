# Models

- [Extend BumbleModel](#extendbumblemodel)
- [Add your model to `config/bumble.php`](#addingmodels)
- [Base Models](#basemodels)
- [Tenant Models](#tenantmodels)
- [Show a model in the top navigation](#topnav)
- [Hide a model from the side navigation](#sidenav)
- [Show a description for a model](#description)

<a name="extendbumblemodel"></a>
## 1. Extend `BumbleModel`
To configure a model for use within Bumble's admin, all models you wish to use inside Bumble have to extend `Monarkee\Bumble\Models\BumbleModel`. This base class extends Eloquent and sets up all of the necessary groundwork needed by the CMS. If you use a "base model" for your models, make sure it extends `BumbleModel` as well.

<a name="addingmodels"></a>
## 2. Add your model to `config/bumble.php`
Each models needs to be registered inside of Bumble's configuration file under the `models` key. The key to your model class should be the singular, hyphenate slug version of the model's name. For instance, if you were registering a `User` model, you would register it like so:

    'models' => [
        'user' => 'App\User'
    ],

And, if you were registering an `InvoiceItem`, you would use this:

    'models' => [
        'invoice-item' => 'App\InvoiceItem'
    ],

<a name="basemodels"></a>
## Use BaseModels with Bumble

Your models can inherit from a BaseModel of your own creation. All you have to do is be sure it extends `Monarkee\Bumble\Models\BumbleModel`.

<a name="tenantmodels"></a>
## Handling Tenant Models

Some apps limit Eloquent queries by a tenant column, either a `user_id` or some other `tenant_id`. This is often implemented with a trait. An example of this is the [Laravel Multi Tenant](https://github.com/AuraEQ/laravel-multi-tenant) package. When you log into Bumble with a user, your models may be automatically limited by this functionality. To get around this, the BumbleModel overrides the booting of traits. If you'd like the still limit the admin by tenants, on your model set the `$enableTraits` property to `true`.

    public $enableTraits = true;

<a name="topnav"></a>
## Show a Model In The Top Navigation
To show your model in the top navicatoin, simply define a public `$showInTopNav` property and set it to `true`.

    public $showInTopNav = true;

<a name="sidenav"></a>
## Hide a Mode From The Side Navigation
Sometimes, you may want to keep a model hidden from the side navigation but still usable within the system. You can simply set the `$showInSideNav` to `false`:

    public $showInSideNav = false;

<a name="description"></a>
## Show a Description For a Model
This allows you to add a helpful description on a models create page under the header.

    public $description = 'Pages for the different sections of the website';

## Showing the Title of the Entry Being Edited
This enables you to set the column that is showing in the main heading of an entry's edit page. Defaults to the entry's title column, if one exists.

    public $editingTitle = 'slug' // Will show the value of the slug column