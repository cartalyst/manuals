###Widgets and Plugins

----------

Widgets and Plugins are new systems we've built into Laravel.  We feel that our system is really powerful and easy to use. Widgets are used pull in generated views, while plugins will be used to pull in and store requested data to manipulate as you wish.

----------

#### Creation

----------

To create a widget or plugin, you just need to create a standard class with the appropriate namespace.  We'll use users as an example again with some additional comments to explain the structure and code. The example below is all you need to create a widget or plugin.

	<?php

	/**
	 * Namespace
	 * Extensions should always be contained in a namespace, copying the folder structure
	 * of your extension.  So if your extensions directory name is foo, you should have a
	 * namespace of Foo.  In terms of widgets and plugins, you add an additional Plugins
	 * or Widgets namespace to the end.  So Foo becomes Foo\Widgets or Foo\Plugins.
	 * Since our users extension is in a containing Platform folder, our namespace for
	 * Widgets is Platform\Users\Widgets
	 */
	namespace Platform\Users\Widgets;

	use API;
	use Theme;

	/**
	 * Class
	 * Your class name is mainly used to organize your widgets.  Since we are creating
	 * a form widget here, we named our class Form.
	 */
	class Form
	{
		/**
		 * Method
		 * The method will contain the logic for your widget/plugin. A Widget should always
		 * return a theme or view file, while a plugin should always return a data object.
		 * Both widgets and plugins can accept parameters.
		 */
		public function edit($id)
		{
			// get user being edited
			$user = API::get('users/1');

			...

			return Theme::make('platform/users::widgets.form.edit', $data);
		}

	}

> **Note:** to make a plugin instead of a widget, you just need to change the Widgets namespace to Plugins and move the file into the plugins directory. **

----------

#### Usage

----------

Now that we have created a widget or plugin, we need to know how to call it.  To do this, we took advantage of Laraval's blade extending. To call a widget or plugin is as simple as calling `@widget('key')` or `@plugin('key')`. Your key will essentially be the path to your widget or plugin.

To call our Form Edit widget, we would do the following call in our view.

	@widget('platform/users::form.edit', 5);

There are 2 main sections to the widget or plugins key, before and after the `::`.

Everything that falls before the `::` is the namespace path to your extensions widgets, minus the widget/plugin namespace.  Since the namespace for our widget in this example is `Platform\Users\Widgets`, that means our namespace portion of the key will be `platform/users`.

The 2nd portion of the key is everything that falls afer the `::`. This section simply is your class name and method name.  In our example, we use the class name of `Users` and method of `edit`, so our key portion becomes `users.edit`.

Now that you have your 2 key portions, you just combine them with `::`. So now our key becomes `platform/users::form.edit`;

> **Note:** if you use subdirectories to organize your widget and plugins folder, use the PSR-0 naming convention.  This means you append your directory structure to the beginning of your class name with a `_` seperator.  A structure of `widgets\groups\form.php` will have the class name of `Groups_Form`. The new widget call would be @widget('platform/users::groups.form.edit');


----------

#### Parameters

----------

Paramaters with widgets and plugins are slightly different. With widgets, the parameters that get passed to your widget method start with the 2nd paramater in your widget call.

	@widget('vendor/key', 'your params start here', 'and continue');

With Plugins, they don't start until your 3rd param.

	@plugin('vendor/key', 'something', 'your params start here', 'and continue');

But why is that? Well plugins are made to return data, so we use the 2nd paramater as the variable to store your data in.  So if your plugin retrieves an array of users, you would do something like this:

	// We'll say this plugin grabs the last 5 registered users
	@plugin('platform/users::users.registered.last', 'users', 5)

	// Now those 5 users are stored in the $users variable
	// We'll loop through the array and do something with it
	@foreach ($users as $user)

		// do something with the data you recieved
		...

	@endforeach
