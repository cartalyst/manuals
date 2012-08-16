###Introduction

----------

When building an extension, it's more than likely you will want to have some [configurable options](http://daylerees.com/2012/04/13/laravel-configuration/).

Config files are PHP files that return an array. They're stored under `path/to/extension/config`.

For simplicity, our extension will have one configuration file, located under `books/config/books.php`:

	<?php

	return array(

		// Returns the path of the book covers.
		// this path is relative to path('public')
		'covers_path' => 'books'.DS.'covers',
	);

----------
