## Authentication

Laravel's authentication feature is supported out-of-the-box, and you may use your own ```User``` Eloquent model. To make it so Bumble can use your User model, simple add ```use BumbleUserTrait;``` to it. This allows the CMS to get the full name of the user and the [Gravatar](http://gravatar.com) for the user.