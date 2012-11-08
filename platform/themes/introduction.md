###Introduction

----------

####What Are Themes?
Themes allow you to "skin" or change the look of your Platform application.

Platform allows you to change much more than the style of your application through it's theme class. We built Platform to be designer friendly and as a result of this, designers have the power to change the applicatin without knowing complex object-orientated PHP. With HTML, CSS (or [LESS](http://less.org) if you're not still partying like it's 1999) and a bunch of expressive helper tags you can fully customize your app.

You can create an unlimited amout of themes in Platform. To get you going though, we've created two `default` themes for you, one for the frontend of cartalyst and one for the backend (admin) area.

You can create your own themes that extend our default themes, giving you the option to override just one `template` file or overriding every single file.

####Theme Structure

A platform theme is structured like so:

	name
	|  asseets
	|  |  css
	|  |  img
	|  |  js
	|  extensions
	|  |  vendor1
	|  |  |  extension1
	|  |  |  |  assets
	|  |  |  |  |  css
	|  |  |  |  |  img
	|  |  |  |  |  js
	|  |  |  |  template1.blade.php
	|  |  |  |  template2.blade.php
	|  |  |  extension2
	|  |  vendor2
	|  |  |  extension3
	|  templates
	|  |  default.blade.php
	|  theme.info

#####But wait, I'm Lost!

Let's explain the files required in a Platform theme in a little more detail:

1. `name` is the name of your theme
2. `name/assets` is the global assets folder. Any assets that should / could be shared between extensions should be placed here.
3. `name/extensions` is a folder in which we place all of our extensions' theme files within.
4. `name/extensions/vendor1` is an example vendor. As of Platform 1.1, extensions are organized into vendors.
4. `name/extensions/vendor1/extension1` is an example extension. It has the following file structure:
   - `assets` is the folder within the extension where all it's assets live. This folder's contents are the same as the `name/assets` folder listed earlier.
   - `template1.blade.php` is an extension's template file. It contains HTML, helper tags and commands to add assets to the template.
5. `name/templates/default.blade.php` is the default template your extension files will extend. We'll cover this more in depth later on. We use Laravel's [Blade templating engine](http://laravel.com/docs/views/templating) for our templates, but you don't have to.
6. `theme.info` is a [JSON encoded](http://en.wikipedia.org/wiki/JSON) information file about the theme. This includes properties such as the theme's name, author, description and version in addition to an unlimited amount of theme options that can allow users to customize your theme.

----------
