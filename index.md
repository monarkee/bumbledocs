## Bumble Documentation

Bumble is a Laravel package that aims to be your go-to CMS package. It strives to provide an easy-to-use administration interface, flexible data modeling via FieldTypes, and data portability by not holding your data hostage.

## Easy To Use Administration

One of the design goals of Bumble was to enable you to use all of the good things about Laravel, but have an auto-generated administration interface. So we encourage you to use all of the great features of Laravel like migrations, authentication, and controllers.

## Flexible Data Modeling

A CMS lives and dies by its ability for users to edit data easily and quickly. We think a CMS package should have a wide range of field types and widgets to make editing that data a breeze. If we don't have a field that does what you need, then we have a plugin system that makes creating your own custom fields and views simple. And we're always looking to improve it.

Getting your data out of the system shouldn't be a pain either. It shouldn't require learning another templating system or vendor-specific syntax. So we've built Bumble to enable you to use Laravel's controllers and Blade templating as a default. In fact, since Bumble is simply a Laravel composer package, you don't have to use it at all. You could create your entire app and install Bumble at the end. Or you can start with Bumble at the beginning to enable you to set up your models for clients to input data as you build out the heavier portions of the site.

## Data Portability

Many CMS systems limit your website's future extensibility by coupling you to their database schema. For example, in a lot of systems your data might be stored in a `posts` or `content` table and the custom fields might be stored as columns on that gigantic table. When it comes time to convert your site into a full-fledged app, you're stuck with the task of working with the CMS to get your data out, or you'll have to migrate all of it yourself to a more conventional database schema.

With Bumble, the goal is the opposite. We believe you should be able to get rid of Bumble at any time and still have a usable database. We want you to use your Laravel migrations to create individual tables to go with your Eloquent models, just like you normally would.