###Model

----------

Creading models using the [Platform Crud](/manuals/crud) allows us to have an implementation of the [Active Record Pattern](http://en.wikipedia.org/wiki/Active_record_pattern) without the bloat of a full-blown ORM.

Navigate to `books/models` and create a file called `book.php`. This will be our Crud model that represents a book entity throughout our extension.

It's table name will be books, it will use timestamps and has a bunch of [Validation Rules](http://laravel.com/docs/validation) that allow us to control the data that comes into our model before persisting it to a database.

Our `model.php` file should look something like below:

	<?php
	
	namespace Books;

	use Crud;
	
	class Book extends Crud
	{
	
		/**
		 * The name of the table associated with the model.
		 *
		 * @var string
		 */
		protected static $_table = 'books';
	
		/**
		 * Indicates if the model has update and creation timestamps.
		 *
		 * @var bool
		 */
		protected static $_timestamps = true;
	
		/**
		 * Validation rules for model attributes.
		 *
		 * @var array
		 */
		protected static $_rules = array(
			'title'  => 'required',
			'author' => 'required',
			'link'   => 'url',
			'price'  => 'numeric',
			'year'   => 'numeric',
		);
	
	}


----------
