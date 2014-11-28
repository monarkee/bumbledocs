## Model Configuration

### 1. Extend ```BumbleModel```

To configure a model for use within Bumble's admin, all models you wish to use inside Bumble have to extend ```Monarkee\Bumble\Models\BumbleModel```. This base class extends Eloquent and sets up all of the necessary groundwork needed by the CMS. If you have a "base model" you use for your models, make sure it extends ```BumbleModel``` as well.

### 2. Setting Up Validation

Validation is not required for using a model in Bumble. This is done as a convenience for those times when you're just getting started and wish to input content from a trusted source.

To get started setting up your model's validation, add a ```$validation``` property to your model. This should be set to an array of validation rules as you would use with Laravel's validator. See the section on Validation in the [Laravel Documentation](http://laravel.com/docs/4.2/validation#available-validation-rules) to find rules you can use for your models.

### 3. Implement a ```setFields()``` Method

When your model is instantiated inside of Bumble, it expects a ```setFields()``` method to be available and will call the method on creation. Here's an example of a model with one [Fieldset](/docs/fieldsets) and two [FieldTypes](/docs/fieldtypes):

public function setFields()
{
return new Fieldset([
new TextField('title'),
new SlugField('slug', ['set_from' =&gt; 'title'])
]);
}

Notice how we're simply returning a new ```Fieldset``` object, which accepts an array of new ```FieldType``` objects. To set up an interface with two tabs, we simply set it up like so:

public function setFields()
{
return new Fieldset([
'tab-one' =&gt; [new TextField('title')],
'tab-two' =&gt; [new SlugField('slug', ['set_from' =&gt; 'title'])]
]);
}

&gt; Note: Each key in the array is used as the title for the tab in the editor.

## BaseModels

Your models can inherit from a BaseModel of your own creation. All you have to do is be sure it extends ```Monarkee\Bumble\Models\BumbleModel```.