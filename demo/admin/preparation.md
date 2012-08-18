###Preparing Our Controller

----------

Each extension with an admin interface needs an admin controller. Navigate to `books/controllers/admin` and create a file called `books.php`. This is our main admin controller's name.

Our controller will allow us to manage the CRUD aspect of our extension; it will:

- List all books
- Create a book
- Update a book
- Save a book
- Delete a book

To get us started, we should 

	<?php

	class Books_Admin_Books_Controller extends Admin_Controller
	{
	
		/**
		 * This function is called before the action is executed.
		 *
		 * @return void
		 */
		public function before()
		{
			
		}
	
		/**
		 * This is the screen that lists all the books.
		 *
		 * @return  Response
		 */
		public function get_index()
		{
			
		}
	
		/**
		 * This action is an alias to get_edit(). We
		 * will just not pass an ID to the edit screen
		 * so it allows us to create the book.
		 *
		 * @return  Response
		 */
		public function get_create()
		{
			
		}
	
		/**
		 * This action contains the books edit screen.
		 *
		 * @return  Response
		 */
		public function get_edit($id = false)
		{
			
		}
	
		/**
		 * Alias for post_edit() without an ID
		 * passed to it.
		 *
		 * @return  Redirect
		 */
		public function post_create()
		{
			
		}
	
		/**
		 * This screen is the POST method for editing
		 * or creating a book. It makes a call to the
		 * API to edit or create the book and redirects
		 * accordingly.
		 *
		 * @return  Redirect
		 */
		public function post_edit($id = false)
		{
			
		}
	
		/**
		 * Delets a book by the given ID and returns
		 * back to the list page.*
		 *
		 * @return  Redirect
		 */
		public function get_delete($id)
		{
			
		}
	
	}

From here, we can jump right in and edit the `before()` method. In this method, we're going to be setting the active menu item. This item was created back when we were [Preparing our Migrations](/manuals/demo/data#migrations).

	public function before()
	{
		// Always call the parent function. This
		// helps us keep compatibility when
		// Platform is upgraded, should Platfom
		// use the parent method we're overriding.
		parent::before();

		// The parameter here must match the slug
		// of a menu item that exists.
		$this->active_menu('admin-books-list');
	}

----------
