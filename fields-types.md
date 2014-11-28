# Field Types


### FieldTypes

- [FieldType Basics](#fieldtype-basics)
- [Adding Fields To Your Model](#adding-fields)

<a name="fieldtype-basics"></a>
### FieldType Basics

Bumble comes with a selection of built-in field types you can use to edit your data in the CMS.

new Field([
'show_in_listing' =&gt; true, // Show the field in the editor
'placeholder' =&gt; 'Placeholder value' // Used in the input
])


<a name="adding-fields"></a>
### Adding Fields To Your Model

All fields should be added to a new Fieldset object. The name of the field is the first argument, which is used to assign its column and label in editor.

new Fieldset([
new TextField('title')
]);

You can also set options to the field by passing an array in the second argument.

new Fieldset([
new TextField('title', ['widget' =&gt; 'WYSIWYGField'])
]);

### Changing the Widget Type of a field

You can swap out the field's widget with another by specifying a ```widget``` option.

___

## FieldTypes

- [TextField](#textfield)
- [SlugField](#slugfield)
- [TextareaField](#textareafield)
- [PasswordField](#passwordfield)
- [BooleanField](#booleanfield)
- [FileField](#filefield)
- [S3FileField](#s3filefield)
- [HasOneField](#hasonefield)
- [DateTimeField](#datetimefield)
- [BelongsToManyField](#belongstomanyfield)
- [TagsField](#tagfield)

<a name="textfield"></a>
### TextField

This is a basic text field. You can create a TextField like this:

new TextField('column_name');

<a name="slugfield"></a>
### SlugField

A SlugField is just like a TextField, except it has a few special powers. It can automatically set its value from the text of another field by setting its ```set_from``` parameter:

new SlugField('slug', ['set_from' =&gt; 'title']);

When you save this model, it will take the value from the ```title``` key in the input, and set the value of ```slug``` to that.


<a name="textareafield"></a>
### TextAreaField

A TextAreaField is just like a TextField, except it uses the TextareaField widget type.

new TextareaField('content')

To use a WYSIWYG, you can change the field's widget type:

new TextareaField('content', ['widget' =&gt; 'WYSIWYGField']

<a name="passwordfield"></a>
### PasswordField

A password field is a FieldType that can be used to set passwords and hash them using Larave's Hash::make(). Don't forget you can opt to use your own mutator and Bumble will use that in instead. You would need to disable the default hashing behavior by setting the ```hash``` option to ```false```.

<a name="booleanfield"></a>
### BooleanField

This field is represented in the database as a 1 or a 0 (binary) value. It provides a check box and is given a label based on the title you pass through.

new BooleanField('active')

<a name="filefield"></a>
### FileField

FieldFields are used to upload files to a directory on the server. The filename will be saved to the column in the database.

new FileField('file', [
'upload_to' =&gt; 'files',
'anonymize' =&gt; true,
'unlink_on_delete' =&gt; true
)

This will create a new FieldField, upload the files to ```public/files```, generated a unique filename, and delete the files when the row is deleted.

&gt; Note: By default, filenames are not anonymized, and files are not deleted.

<a name="s3filefield"></a>
### S3FileField

S3FileFields are similar to FileFields, except they have the ability to upload to Amazon S3.

new S3FileField('image', [
'bucket_name' =&gt; 'images' // Uses your default bucket set in your config if not set here
'upload_to' =&gt; 'banners'
])

<a name="hasonefield"></a>
### HasOneField

Coming soon.

<a name="datetimefield"></a>
### DateTimeField

DateTimeFields are used for modifying MySQL's DateTime column type. It uses the [XDSoft DateTimePicker](http://xdsoft.net/jqplugins/datetimepicker/) on the input, which gives you a nice way to edit the field.

new DateTimeField('published_at')

You can also specify how the date is shown in the listing by passing the ```format``` and giving it a valid PHP date format, like so:

new DateTimeField('published_at', ['format' =&gt; 'D F d, Y'])


<a name="belongstomanyfield"></a>
### BelongsToManyField

Coming soon.

<a name="tagfield"></a>
### TagField

Coming soon.
