###Requirements

----------

As stated before, Extensions are just Laravel bundles at the core with a few additional requirements and friendly additions.

----------

####Extension.php file

In addition to your base bundle folder setup, you will also need an extension.php file in your extensions root folder.  This file sets several configurable options for our extension that Platform will hook into. These options include extension info, dependencies, bundle settings, used events, event listeners, global routes and rules.

Here is an example extension.php file for a users extension.

	<?php

	return array(

		'info' => array(
			'name'        => 'Users',
			'slug'        => 'users',
			'author'      => 'Cartalyst LLC',
			'description' => 'Manages your website users, groups and roles.',
			'version'     => '1.0',
			'is_core'     => true,
		),

		'dependencies' => array(
			'menus',
		),

		'bundles' => array(
			'handles' => 'users',
			'location' => 'path: '.__DIR__,
		),

		'events' => array(
			'user.create',
			'user.update',
			'user.delete',
			'group.create',
			'group.update',
			'group.delete',
		),

		'listeners' => function() {
			Event::listen('extension1.event', function() { ... });
			Event::listen('extension2.event', funciton() { ... });
		},

		'global_routes' => function() {
			Route::any(ADMIN.'/login', 'users::admin.users@login');
			Route::any(ADMIN.'/logout', 'users::admin.users@logout');
		},

		'rules' => array(
			'random_rule',
			'users::admin.users@index',
			'users::admin.users@create',
			'users::admin.users@edit',
			'users::admin.users@delete',
			'users::admin.groups@index',
		),

	);

- `info` The info array stores basic information about your extension.  This will be pulled into the database during installation.

- `dependencies` The dependencies array contains a list of extensions that the current extension requires.

- `bundles` The bundles array is what you are accustomed to seeing in the main application bundle's bundle.php file.  Instead of manually adding each extension you have into that file, we made more modular friendly to where you can add the settings here instead.

- `events` The events array contains the names of events your extension fires.  Creating this array of events for your extension allows other extensions to see what events your extension uses.  This comes in handy for extensions that may want to capture all of another extensions events, or every event in the system.  They can now build listeners dynamically rather than manually.

- `listeners` Does your extension want to listen to events other extensions may be firing? Throw them into this listeners function so Platform knows that your extension wants to do something when those events. Platform scans for and registers these events for you. *Note: These listeners are contained in a function rather than an array*.

- `global_routes` Each extension can still have its own routes.php file which can contain routing logic for that specific extension. But, what if you want to also add routes to the global routing? Thats what global routes are for.  These routes will be equivalent to the routes you put into the main application bundle's route.php file.  They are loaded after the main applications bundle route though. *Note: These routes are contained in a function rather than an array*.

- `rules` The rules array contains rules, or permissions users must have, in order to view a certain area of your extension.  How rules work you can find out in the Sentry portion of our documentation.  Simply put though, if you want to add a rule to your extension, you add it to this array.

----------
