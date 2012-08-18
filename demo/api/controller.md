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
		 *	<code>
		 *		$all_books = API::get('books');
		 *		$a_book    = API::get('books/1');
		 *	</code>
		 *
		 * @param   int   $id
		 * @return  Response
		 */
		public function get_index($id = false)
		{
			
		}
	
		/**
		 * Creates a book.
		 *
		 *	<code>
		 *		$book = API::post('books', $data);
		 *	</code>
		 *
		 * @return  Response
		 */
		public function post_index()
		{
			
		}
	
		/**
		 * Updates an existing book.
		 *
		 *	<code>
		 *		$book = API::put('books/1', $data);
		 *	</code>
		 *
		 * @param   int   $id
		 * @return  Response
		 */
		public function put_index($id)
		{
			
		}
	
		/**
		 * Deletes a book.
		 *
		 *	<code>
		 *		API::delete('books/1');
		 *	</code>
		 *
		 * @param   int  $id
		 * @return  Response
		 */
		public function delete_index($id)
		{
			
		}
	
		/**
		 * Returns information necessary to
		 * make a datatable.
		 *
		 * @return  Response
		 */
		public function get_datatable()
		{
			
		}
	
		/**
		 * Processes file uploads for a cover
		 * and returns the cover name. This method
		 * is used by both post_index() and
		 * put_index(). Keeping things DRY, we'll
		 * put this common action in it's own method.
		 *
		 * @return  string
		 */
		protected function process_cover_upload()
		{
			
		}
	
	}

	
####get_index()

In the `get_index()` method, we either need to return an individual book (if one is requested) or return an array of books.

Below is one approach we could take to achieving this:

	public function get_index($id = false)
	{
		// If an ID was provided, we're going to
		// be finding an individual book.
		if ($id)
		{
			// Find the book
			$book = Book::find($id);

			// Boook not found? Return
			// an appropriate Response
			if ($book === null)
			{
				return new Response(array(
					'message' => Lang::line('books::books.errors.not_found')->get(),
				), API::STATUS_NOT_FOUND);
			}

			// Return the book
			return new Response($book);
		}

		// Otherwise return all books
		return new Response(Book::all());
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

		// Look for a cover - this method is shared
		// between this method and put_index()
		if ($cover = $this->process_cover_upload())
		{
			$book->cover = $cover;
		}

		// Get the result (which is the
		// number of records affected) by
		// saving a book
		if ($result = $book->save())
		{
			return new Response($book);
		}

		// If the result is 0, no records were
		// updated. Therefore, the book was not
		// updated.
		else
		{
			return new Response(array(

				// Return a general error message
				'message' => Lang::line('books::books.create.error')->get(),

				// This is a shorthand IF statement which returns
				// validation errors if they're present.
				'errors'  => ($book->validation()->errors->has()) ? $book->validation()->errors->all() : array(),
			),

			// Like the 'errors' key above, we return an appropriate
			// API status according to whether there are validation
			// errors present.
			($book->validation()->errors->has()) ? API::STATUS_BAD_REQUEST : API::STATUS_UNPROCESSABLE_ENTITY);
		}
	}

####put_index()

This method is identical to `post_index()` except that we need to find a book to update.

	public function put_index($id)
	{
		// Try find the book they're after
		$book = Book::find($id);

		// No book?
		if ($book === null)
		{
			return new Response(array(
				'message' => Lang::line('books::books.errors.not_found')->get(),
			), API::STATUS_NOT_FOUND);
		}

		// Check if the cover is gone
		if (isset($book->cover) and ! Input::get('cover'))
		{
			// File::delete() checks for
			// existence of the file.
			File::delete(str_finish(path('public'), DS).str_finish(Config::get('books::books.covers_path'), DS).$book->cover);
		}

		// Update the attributes
		$book->fill(Input::get());

		// Look for a cover
		if ($cover = $this->process_cover_upload())
		{
			$book->cover = $cover;
		}

		// Get the result (which is the
		// number of records affected) by
		// saving a book
		if ($result = $book->save())
		{
			return new Response($book);
		}
		else
		{
			return new Response(array(
				'message' => Lang::line('books::books.update.error')->get(),
				'errors'  => ($book->validation()->errors->has()) ? $book->validation()->errors->all() : array(),
			), ($book->validation()->errors->has()) ? API::STATUS_BAD_REQUEST : API::STATUS_UNPROCESSABLE_ENTITY);
		}
	}

####delete_index()

This method is used to delete a book with the given ID. If successful, we don't return any content, but rather a successful "No content" status.

	public function delete_index($id)
	{
		// Find the book
		$book = Book::find($id);

		// No book?
		if ($book === null)
		{
			return new Response(array(
				'message' => Lang::line('books::books.errors.not_found')->get(),
			), API::STATUS_NOT_FOUND);
		}

		// If there is a cover registered with the book,
		// delete the file.
		if (isset($book->cover))
		{
			// File::delete() checks for
			// existence of the file.
			File::delete(str_finish(path('public'), DS).str_finish(Config::get('books::books.covers_path'), DS).$book->cover);
		}

		// Delete the book
		$book->delete();

		// Return a 'No content' status. 'No content' is
		// a successful status (204) however there is just
		// no relevent data to pass to the client.
		return new Response(null, API::STATUS_NO_CONTENT);
	}



####get_datatable()

This method returns a complex response containing an array of items used in the datatable. The comments will explain the logic behind it. What you need to focus on is the `$defaults` param in it:

	public function get_datatable()
	{
		// Generate an array of default Platform Table
		// query parameters.
		$defaults = array(
			'select'   => array(
				'id'          => Lang::line('books::books.general.id')->get(),
				'title'       => Lang::line('books::books.general.book_title')->get(),
				'author'      => Lang::line('books::books.general.author')->get(),
				'price'       => Lang::line('books::books.general.price')->get(),
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
		return new Response(array(

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
		));
	}

####process_cover_upload()

This method is a shared method by `post_index()` and `put_index()` to upload and manage new book covers.

	protected function process_cover_upload()
	{
		// Look if the person has uploaded a
		// cover for the book. If so, we'll
		// continue to process it
		if (Input::has_file('cover'))
		{
			// Make sure the covers path exists
			// so we can save the cover there.
			File::mkdir(Book::covers_path());

			// Get the uploaded file's information
			$file = Input::file('cover');
			$name = $file['name'];

			// If the file exists, we need to find a new home
			// for it. We'll do this by appending an underscore
			// followed by incrementing numbers until the file does
			// not exist. For example, if the user uploaded "image.png"
			// and it already exists, we'll name it "image_1.png". If that
			// exists, we'll name it "image_2.png" and so on.
			if (File::exists(str_finish(Book::covers_path(), DS).$file['name']))
			{
				// Get an array containing all
				// information about the file (such as the
				// filename and extension)
				$name_parts = pathinfo($name);

				// Flag for existence
				$exists = true;

				// Counter that's incremented to add numbers
				// to the filename
				$i = 1;

				// Loop keeps running while the file exists
				while ($exists === true)
				{
					// Get a name to test against the file system
					$test_name = $name_parts['filename'].'_'.$i++.'.'.$name_parts['extension'];

					// If the file doesn't exist, set our final name
					// to the name we've tested against the file system.
					// Then, break our loop
					if ( ! File::exists(str_finish(Book::covers_path(), DS).$test_name))
					{
						$name   = $test_name;
						$exists = false;
					}
				}
			}

			// Use Laravel's helper methods to upload the file.
			if (Input::upload('cover', Book::covers_path(), $name))
			{
				return $name;
			}
		}
	}

There you go! You've made your first API controller.

----------
