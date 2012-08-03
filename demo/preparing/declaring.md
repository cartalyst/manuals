###Declaring

----------

>**Notes:** As outlined before, this tutorial assumes you are familiar with the different components of an extension. If you're new to Platform, see our [Extension Guide](/manuals/platform/extensions) first.

####Creating a folder for our extension

In Platform, an extension's files live in 3 places:

1. PHP files live under `platform/extensions`
2. Backend templates live under `public/platform/themes/backend/default/extensions`
3. Frontend templates live under `public/platform/themes/frontend/default/extensions`

Locate the `platform/extensions` folder within your Platform installation. Create a folder called `books` (this is case sensitive). This is where our extension PHP files are going to live.

>**Notes:** You can create a sub-folder structure in order to group extensions if you wish. For example, if your company is called `Webcomm`, you might have a the following folder structure for your `books` extension - `platform/extensions/webcomm/books`. Currently, you can only nest extensions in folders **one level deep**.

####Creating our extension.php file

Navigate to your extension's folder. Create a new file in it called `extension.php`. Insert the code below into your file using your [favorite text editor](http://www.sublimetext.com):

	<?php
	return array(
	    'info' => array(
	    
	    	// Give your extension a name - This
	    	// is what is shown to your users in
	    	// the Extensions Manager
	        'name'        => 'Books',
	        
	        // Slug - MUST match the folder name
	        // you put the extension in.
	        'slug'        => 'books',

			// Author - you're creating this extension,
			// so take some credit for it
	        'author'      => 'Cartalyst LLC',

			// Write a one or two sentence description
			// about your extension
	        'description' => 'A books management extension',

			// Version of the extension
	        'version'     => '1.0',
	    ),

		// Because extensions are Laravel Bundles with a
		// bit of sugar and spice, we need to register
		// the Laravel Bundle.
	    'bundles' => array(
	        'handles' => 'books',
	        'location' => 'path: '.__DIR__,
	    ),

		// We could register event listeners to be executed
		// whenever our extension is installed and enable
	    'listeners' => function() {

			// Feel free to delete all this
			Event::listen('laravel.query', function($sql, $bindings, $time)
			{
				Log::query($sql.' '.json_encode($bindings));
			});

	    },
	);

It is ideal to have a read through the comments in the code to grasp an understanding of each component's role within an extension.

----------
