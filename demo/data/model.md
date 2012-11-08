###Model

----------

Creading models using the [Platform Crud](/manuals/crud) allows us to have an implementation of the [Active Record Pattern](http://en.wikipedia.org/wiki/Active_record_pattern) without the bloat of a full-blown ORM.

Navigate to `books/models` and create a file called `book.php`. This will be our Crud model that represents a book entity throughout our extension.

It's table name will be books, it will use timestamps and has a bunch of [Validation Rules](http://laravel.com/docs/validation) that allow us to control the data that comes into our model before persisting it to a database.

Our `model.php` file should look something like below. It's essentially a pretty bare model, with a couple of callbacks to enhance data in the model, plus a helper method:

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
		
		/**
		 * Returns the covers path for a book.
		 *
		 * @return  string
		 */
		public static function covers_path()
		{
			return str_finish(path('public'), DS).Config::get('platform/books::books.covers_path');
		}

		/**
		 * Gets called before insert() is executed to modify the query
		 * Must return an array of the query object and columns array($query, $columns)
		 *
		 * @param   Query  $query
		 * @param   array  $columns
		 * @return  array
		 */
		protected function before_insert($query, $columns)
		{
			// Strip out the data added in the after_find()
			// and after_all() callbacks.
			array_forget($columns, 'cover_path');
			array_forget($columns, 'cover_url');

			return array($query, $columns);
		}

		/**
		 * Gets called before update() is executed to modify the query
		 * Must return an array of the query object and columns array($query, $columns)
		 *
		 * @param   Query  $query
		 * @param   array  $columns
		 * @return  array
		 */
		protected function before_update($query, $columns)
		{
			// Strip out the data added in the after_find()
			// and after_all() callbacks.
			array_forget($columns, 'cover_path');
			array_forget($columns, 'cover_url');

			return array($query, $columns);
		}

		/**
		 * Gets call after the find() query is exectuted to modify the result
		 * Must return a proper result
		 *
		 * @param   Query  $query
		 * @param   array  $columns
		 * @return  array
		 */
		protected function after_find($result)
		{
			// If we have a valid book cover, attach some
			// more properties
			if (isset($result->cover) and $result->cover and File::exists($cover_path = str_finish(static::covers_path(), DS).$result->cover))
			{
				$result->cover_path = $cover_path;
				$result->cover_url  = URL::to_asset(str_replace(DS, '/', str_finish(Config::get('platform/books::books.covers_path'), DS).$result->cover));
			}

			return $result;
		}

		/**
		 * Gets called after the all() query is exectuted to modify the result
		 * Must return a proper result
		 *
		 * @param   array  $results
		 * @return  array  $results
		 */
		protected static function after_all($results)
		{
			// Loop through results
			foreach ($results as &$result)
			{
				// Append additional data
				if (isset($result->cover) and $result->cover and File::exists($cover_path = str_finish(static::covers_path(), DS).$result->cover))
				{
					$result->cover_path = $cover_path;
					$result->cover_url  = URL::to_asset(str_replace(DS, '/', str_finish(Config::get('platform/books::books.covers_path'), DS).$result->cover));
				}
			}

			return $results;
		}
	
	}


----------
