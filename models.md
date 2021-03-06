# Models

- [Extend BumbleModel](#extendbumblemodel)
- [Add your model to `config/bumble.php`](#addingmodels)
- [Base Models](#basemodels)
- [Tenant Models](#tenantmodels)

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
