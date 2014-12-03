# Fields

Fields are just objects which handle displaying content from your database, giving you a view in the admin, and process data inputted from request. They handle things like:

* Knowing which database column they belong to
* Showing placeholders in form elements
* Setting up which Field Widgets to use
* Displaying help text
* Processing input data into the correct format for saving to the database

### FieldTypes

- [FieldType Basics](#fieldtype-basics)
- [Adding Fields To Your Model](#adding-fields)

<a name="fieldtype-basics"></a>
### FieldType Basics

Bumble comes with a selection of built-in field types you can use to edit your data in the CMS. Creating them is as simple as newing up the appropriate object and settings its title. The title will be used to set up columns, field labels, and placeholder text:

    new TextField('title')

Most fields have settings you can configure to do things like set upload paths, overriding default columns, etc... You can set those by simply passing in an array of options:

    new SlugField('slug', ['set_from' => 'title'])

All fields should be added to a new Fieldset object on a public `setFields()` method.

    new Fieldset([
        new TextField('title'),
        new SlugField('slug', ['set_from' => 'title'])
    ]);

### Changing the Widget Type of a field

You can swap out the field's widget with another by specifying a `widget` option.

> Note: This can be dangerous if the database column associated with the field doesn't accept the same input type (i.e. using a text-like widget on an integer column). Also beware of FieldTypes that process their data with input of an expected type

___

## Default Field Options

Each field type can be configured with some options that allow you to be very granular in the field's configuration. Here is an example of all the options that can be set on any field:

    new TextField('email', [
        'title' => 'Email' // The name of the field in the admin
        'description' => 'Text Field' // The description of the field
        'placeholder' => 'Enter new Email' // The placeholder text to use in the input
        'column' => 'email_address' // Override the column which is set from the title
        'show_in_listing' => true // Show the field in the entry listing for the model
        'widget' => 'TextareaField' // Override the field's default widget type
        'editable' => true // Set the field's editability
        'default_value' => 'hi@test.com' // Set the field's default value
    ]);

## FieldTypes

- [TextField](#textfield)
- [SlugField](#slugfield)
- [PasswordField](#passwordfield)
- [TextareaField](#textareafield)
- [BooleanField](#booleanfield)
- [FileField](#filefield)
- [S3FileField](#s3filefield)
- [DropdownField](#dropdownField)
- [HasOneField](#hasonefield)
- [BelongsToField](#belongstofield)
- [DateTimeField](#datetimefield)
- [DateField](#datefield)
- [TimeField](#timefield)

<a name="textfield"></a>
### TextField

A text field is the most basic form of input in the system. Below is an example of a TextField:

    new TextField('email', [
        'maxlength' => '25' // Sets the maxlength value on the input
    ]);

<a name="slugfield"></a>
### SlugField

A SlugField is just like a TextField, except it has a few special powers. It can automatically set its value from the text of another field by setting its `set_from` parameter:

    new SlugField('slug', [
        'set_from' => 'title' // Set from the value of the title field
    ]);

When you save this model, it will take the value from the `title` key in the input, process it to be a slug, and set the value of `slug` to that.

<a name="passwordfield"></a>
### PasswordField

A password field is a text FieldType that can be used to set passwords and hash them using Laravel's ```Hash::make()``` method. Don't forget you can opt to use your own mutator for the column and Bumble will use that instead. You would need to disable the default hashing behavior by setting the ```hash``` option to ```false```.

    new PasswordField('password', [
        'hash' => true // Yes, use Bumble's hashing
    ])

<a name="textareafield"></a>
### TextAreaField

A TextAreaField is just like a TextField, except it uses the TextareaField widget type.

    new TextareaField('content', [
        'rows' => 6 // The number of rows the textarea should have
    ])

### Using a WYSIWYG
To use a WYSIWYG editor, you can change the field's widget type like so:

    new TextareaField('content', ['widget' => 'WYSIWYGField']

<a name="booleanfield"></a>
### BooleanField

This field is represented in the database as a 1 or a 0 (binary) value. It provides a check box and is given a label based on the title you pass through.

    new BooleanField('active')

<a name="filefield"></a>
### FileField

FileFields are used to upload files to a directory on the server. The filename will be saved to the column in the database.

    new FileField('file', [
        'upload_to' => 'files', // The path to upload to
        'anonymize' => true, // Anonymize the file name to a random string
        'unlink_on_delete' => true // Whether to delete the file if actually deleting the record
    ])

This will create a new FileField, upload the files to ```public/files```, generate a unique filename, and delete the files when the row is deleted.

> Note: By default, filenames are not anonymized, and files are not deleted.

<a name="s3filefield"></a>
### S3FileField

S3FileFields are similar to FileFields, except they have the ability to upload to Amazon S3. These fields use the S3 configuration details in Bumble's config file.

    new S3FileField('image', [
        'bucket_name' => 'images' // Uses your default bucket set in your config if not set here
        'upload_to' => 'banners' // The path to upload to
    ])

<a name="hasonefield"></a>
### HasOneField

Many times you need to relate your entries to other models. A HasOneField uses the one-to-one relationship

<a name="belongstofield"></a>
### BelongsToField

Many times you need to relate entries to other entries. A BelongsToField uses a Laravel one-to-one relationship with another model. So if you have a user that has one address you can define that field like so:

    new BelongsToField('status'),

<a name="datetimefield"></a>
### DateTimeField

DateTimeFields are used for modifying DateTime column types. It uses the [XDSoft DateTimePicker](http://xdsoft.net/jqplugins/datetimepicker/) on the input, which gives you a nice way to edit the field.

new DateTimeField('published_at')

You can also specify how the date is shown in the listing by passing the ```format``` and giving it a valid PHP date format, like so:

    new DateTimeField('published_at', ['format' => 'D F d, Y'])