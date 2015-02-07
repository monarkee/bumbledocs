# Model Configuration

## 1. Extend `BumbleModel`
To configure a model for use within Bumble's admin, all models you wish to use inside Bumble have to extend `Monarkee\Bumble\Models\BumbleModel`. This base class extends Eloquent and sets up all of the necessary groundwork needed by the CMS. If you use a "base model" for your models, make sure it extends `BumbleModel` as well.

## 2. Add your model to `config/bumble.php`
Each models needs to be registered inside of Bumble's configuration file under the `models` key. The key to your model class should be the singular, hyphenate slug version of the model's name. For instance, if you were registering a `User` model, you would register it like so:

    'models' => [
        'user' => 'App\User'
    ],

And, if you were registering an `InvoiceItem`, you would use this:

    'models' => [
        'invoice-item' => 'App\InvoiceItem'
    ],

## 3. Model Admin

 Bumble stores its configuration in "Model Admin" classes. These classes store validation rules, field configuration, and other CMS-specific parameters. In your model, you reference these classes by implementing a `bumble()` method:

    public function bumble()
    {
        return $this->hasAdmin('InvoiceAdmin');
    }

Simply reference your Model Admin class, and Bumble will do the rest.

## 3. Setting Up Validation

Validation is not required for using a model in Bumble, which is nice for those times when you're just getting started and wish to input content without setting up validation.

To get started setting up your model's validation, add a `$rules` property to your model. This should be set to an array of validation rules just as you would use with Laravel's validator. See the section on Validation in the [Laravel Documentation](http://laravel.com/docs/5.0/validation) to find rules you can use for your models.

## 3. Setting Up Fields

Field definitions are store in `ModelAdmin` classes. When your `ModelAdmin` is instantiated, it requires a `setFields()` method to be implemented that returns a `Fieldset`. Here's an example of a model with one [Fieldset](/docs/fieldsets) and two [FieldTypes](/docs/fieldtypes):

    public function setFields()
    {
        return new Fieldset([
            new TextField('title'),
            new SlugField('slug', ['set_from' => 'title'])
        ]);
    }

Notice how we're simply returning a new `Fieldset` object, which accepts an array of new `Field` objects. To set up an interface with two tabs, pass in an `array` of `Field` objects with a `string` as its key:

    public function setFields()
    {
        return new Fieldset([
            'tab-one' => [new TextField('title')],
            'tab-two' => [new SlugField('slug', ['set_from' => 'title'])]
        ]);
    }

> Note: Each key in the array is used as the title for the tab in the editor.

## Use BaseModels with Bumble

Your models can inherit from a BaseModel of your own creation. All you have to do is be sure it extends `Monarkee\Bumble\Models\BumbleModel`.

## Other Model Configuration Options
- [#topnav](Show a model in the top navigation)
- [#sidenav](Hide a model from the side navigation)
- [#description](Show a description for a model)

There are a couple of other model configuration options available to you. You can

<a name="topnav"></a>
## Show a Model In The Top Navigation
Simply define a public `$showInTopNav` property and set it to `true`.

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