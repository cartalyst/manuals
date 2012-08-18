###Laravel start.php

----------

Remember how we said that every Platform extension is a Laravel Bundle? Well, [Laravel Bundles](http://laravel.com/docs/bundles/) require a `start.php` file if you want to customize behaviour when a Bundle is loaded.

We need to setup some namespaces for our Extension. The namespaces aren't technically necessary, however it's strongly recommended you follow the same convention we have used.

Create a file under `books/start.php` and insert the following:

	Autoloader::namespaces(array(
		'Books\\Widgets' => __DIR__.DS.'widgets',
		'Books\\Plugins' => __DIR__.DS.'plugins',
		'Books'          => __DIR__.DS.'models',
	));

This essentially just registers three namespaces, `Books\Widgets`, `Books\Plugins` and `Books`.

>**Notes:** Although unrelated to Platform, this is a tip that catches many newcomers to coding. The reson there is a double slash `\\` in the code above is so that the slash is escaped. For example, if you used `"some\namespace"`, you're actually using a `\n` which is a new line character. You need to escape the slash with another slash; so `"some\\namespace"`.

----------
