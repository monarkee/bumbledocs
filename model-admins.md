# ModelAdmin Configuration

- [Overview](#overview)
- [Validation](#validation)
- [Setting Up Fields](#fields)
- [Show a model in the top navigation](#topnav)
- [Hide a model from the side navigation](#sidenav)
- [Show a description for a model](#description)

<a name="overview"></a>
## Overview
Bumble stores its configuration in "Model Admin" classes. These classes store validation rules, field configuration, and other CMS-specific parameters. Your model classes have to implement a `bumble()` method which references the class name that stores its configuration:

    use Monarkee\Bumble\Models\BumbleModel;

    // The Model Class
    class User extends BumbleModel {
        public function bumble()
        {
            return $this->hasAdmin('UserAdmin');
        }
    }

Simply reference your Model Admin class, and Bumble will do the rest.

<a name="validation"></a>
## Setting Up Validation

Validation is not required for using a `ModelAdmin` in Bumble, which is nice for those times when you're just getting started and wish to input content without setting up validation.

To get started setting up your `ModelAdmin`'s validation, add a `$rules` property to your `ModelAdmin`. This should be set to an array of validation rules just as you would use with Laravel's validator. See the section on Validation in the [Laravel Documentation](http://laravel.com/docs/5.0/validation) to find the rules you can use.

<a name="fields"></a>
## Setting Up Fields

Field definitions are stored in `ModelAdmin` classes. When your `ModelAdmin` is instantiated, it requires a `setFields()` method to be implemented that returns a `Fieldset`. Here's an example of a model with one [Fieldset](/docs/fieldsets) and two [FieldTypes](/docs/fieldtypes):

    use Monarkee\Bumble\Models\ModelAdmin;

    class UserAdmin extends ModelAdmin {
        public function setFields()
        {
            return new Fieldset([
                new TextField('title'),
                new SlugField('slug', ['set_from' => 'title'])
            ]);
        }
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
