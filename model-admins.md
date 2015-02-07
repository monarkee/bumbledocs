# ModelAdmin Configuration

- [Overview](#overview)
- [Validation](#validation)
- [Setting Up Fields](#fields)

<a name="overview"></a>
## Overview
Bumble stores its configuration in "Model Admin" classes. These classes store validation rules, field configuration, and other CMS-specific parameters. In your model, you reference these classes by implementing a `bumble()` method:

    public function bumble()
    {
        return $this->hasAdmin('InvoiceAdmin');
    }

Simply reference your Model Admin class, and Bumble will do the rest.

<a name="validation"></a>
## Setting Up Validation

Validation is not required for using a model in Bumble, which is nice for those times when you're just getting started and wish to input content without setting up validation.

To get started setting up your model's validation, add a `$rules` property to your model. This should be set to an array of validation rules just as you would use with Laravel's validator. See the section on Validation in the [Laravel Documentation](http://laravel.com/docs/5.0/validation) to find rules you can use for your models.

<a name="fields"></a>
## Setting Up Fields

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
