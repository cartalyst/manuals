###Controller

----------

###Aim

For our API to work, we need to create an API controller.

Our API is going to respond to the following resource paths:
	
	// Reading book(s)
	GET    /api/books
	GET    /api/books/:id

	// Creating a book
	POST   /api/books
	
	// Updating a book
	PUT    /api/books/:id
	
	// Deleting a book
	DELETE /api/books/:id
	
	// Return information for
	// a books datatable
	GET    /api/books/datatable

#####GET /api/books

Return an array of all books

#####GET /api/books/:id

Returns a single book, by the given ID. For example, `/api/books/3` returns a book with the ID, 3.

#####POST /api/books

This method is used to create a book. Information is passed through about the book and we create or update a model instance accordingly and return the created model instance.

#####PUT /api/books/:id

This method is identical to `POST /api/books` except you provide the ID of a book to update.

#####DELETE /api/books/:id

This method is used to delete a book by the given ID.

#####GET /api/books/datatable

This method returns an array of information used for creating a "Platform Table" - an AJAX driven table used for displaying records in the administration interface.

####Creating the Controller

API controllers in Platform work identically to a [RESTful Laravel Controller](http://laravel.com/docs/controllers#restful-controllers). API controllers must extend a base class called `API_Controller`.

Let's get into writing some code! Navigate to `books/controllers/api` and create a file called `books.php`. We'll start by making our methods to correspond to the resource paths:

	<?php
	
	use Books\Book;
	
	class Books_API_Books_Controller extends API_Controller
	{
		/**
		 * Gets either an individual book
		 * or an array of books.
		 *
		 * @return array
		 */
		public function get_index()
		{
			
		}
		
		/**
		 * Creates / updates a book.
		 *
		 * @return  array
		 */
		public function post_index()
		{
		
		}
		
		/**
		 * Returns information necessary to
		 * make a datatable.
		 *
		 * @return  array
		 */
		public function get_datatable()
		{
			
		}
		
	}
	
####get_index()

In the `get_index()` method, we either need to return an individual book (if one is requested) or return an array of books.

Below is one approach we could take to achieving this:

	public function get_index()
	{
		// Check if the person was after
		// a specific book
		if ($id = Input::get('id'))
		{
			// Let's try find a book
			$book = Book::find($id);

			// No book? Let's give an error
			// back to the caller
			if ($book === null)
			{
				return array(
					'status'  => false,
					'message' => Lang::line('books::books.errors.no_book', array(
						'id' => $id,
					)),
				);
			}

			// Found a book? Let's return it
			return array(
				'status' => true,
				'book'   => $book,
			);
		}
		
		// If we have got this far, it's
		// because the person hasn't provided
		// an ID, in which can we will return
		// the entire collection of books
		return array(
			'status' => true,
			'books'  => Book::all(),
		);
	}

####post_index()

In the `post_index()` method, we will accept an array of key / value properties of a Book entity and persists them to the database.

If we were successful, we'll return the book back to the client. If not, we'll try return any validation errors that occured. Otherwise, we'll return a generic error saying the book failed to update.

The method should look something like this:

	public function post_index()
	{
		// Create a book instance from the
		// Input parameters given to the API
		$book = new Book(Input::get());

		// Get the result (which is the
		// number of records affected) by
		// saving a book
		$result = $book->save();

		// If we have any number of records
		// affected (should be 1 record), we
		// return true along with the book
		// entity.
		if ($result)
		{
			return array(
				'status' => true,
				'book'   => $book,
			);
		}

		// If we got validation errors from the book,
		// we return the errors array back ot the caller.
		if ($errors = $book->validation()->errors->all())
		{
			return array(
				'status' => false,
				'errors' => $errors,
			);
		}

		// Otherwise, return a generic message that the
		// book failed to update or create.
		return array(
			'status'  => false,
			'message' => Lang::line('books.'.($book->id ? 'update' : 'create').'.error'),
		);
	}

####get_datatable()

This method returns a complex array of items used in the datatable. The comments will explain the logic behind it. What you need to focus on is the `$defaults` param in it:

	/**
	 * Returns information necessary to
	 * make a datatable.
	 *
	 * @return  array
	 */
	public function get_datatable()
	{
		// Generate an array of default Platform Table
		// query parameters.
		$defaults = array(
			'select'   => array(
				'id'          => Lang::line('books::books.general.id')->get(),
				'title'       => Lang::line('books::books.general.book_title')->get(),
				'author'      => Lang::line('books::books.general.author')->get(),
				'description' => Lang::line('books::books.general.book_description')->get(),
				'year'        => Lang::line('books::books.general.year')->get(),
			),
			'where'    => array(),
			'order_by' => array('id' => 'desc'),
		);

		// Lets get to total book count. This will count the
		// total number of records in the table irrespective
		// of any filters applied to the datatable.
		$count_total = Book::count();

		// Get the filtered count - the count available
		// after filters are applied
		$count_filtered = Book::count('id', function($query) use ($defaults)
		{
			return Table::count($query, $defaults);
		});

		// Set the paging parameter (this is provided by
		// the Table class)
		$paging = Table::prep_paging($count_filtered, 20);

		// Finally, get an array of book objects. We'll modify
		// the query here.
		$items = Book::all(function($query) use ($defaults, $paging)
		{
			list($query, $columns) = Table::query($query, $defaults, $paging);

			return $query;
		});

		// If there were no items, we'll return
		// an array so as to not break the user's
		// iterations.
		$items = ($items) ?: array();

		// Finally, return a big long complex array of
		// data. There is no need to return false here
		// as there is no real way for 
		return array(

			// Status - should always include a status
			'status'         => true,

			// An array of key / value columns (column name / name [localed])
			'columns'        => $defaults['select'],

			// An array of rows for the datatable, which is an array
			// of books (with filters applied)
			'rows'           => $items,

			// Total count of records in table
			'count'          => $count_total,

			// Count of filtered records in the table
			'count_filtered' => $count_filtered,

			// The paging information used in the
			// platform datatable.
			'paging'         => $paging,
		);
	}

There you go! You've made your first API controller.

----------
