###Migrations

----------

Our extension is going to use one table which stores information about our books. The best way to create our table is through [creating migrations](http://laravel.com/docs/database/migrations). Jump into your `books/migrations` folder and create a file called `001_install.php`. Our `books` table will have the following:

- An automatic incrementing field, `id`
- The `title` of the book - string
- The name of the book's `author` - string
- A `description` about the book - text (not required)
- A `link` to the book online - string (not required)
- The book's `price` - decimal number (not required)
- The `publisher` - string (not required)
- Which `year` the book was published - string (not required)
- The path to the book's `cover` image stored on disk - string (not required)

In addition to creating a `books` table, we need to create an admin menu item. It will link to the admin panel for our extension and be called "Books". There is a nice API for creating menu items, demonstrated in the migration below.

How does this all translate into a Laravel migration? Like so:

	<?php

	use Platform\Menus\Menu;
	
	class Books_Install
	{
	
		/**
		 * Make changes to the database.
		 *
		 * @return void
		 */
		public function up()
		{
	
			/* # Create Book Tables
			================================================== */
	
			// Create the books table
			Schema::create('books', function($table)
			{
				$table->increments('id');
				$table->string('title');
				$table->string('author');
				$table->text('description')->nullable();
				$table->string('link')->nullable();
				$table->float('price')->nullable();
				$table->string('publisher')->nullable();
				$table->string('year')->nullable();
				$table->string('cover')->nullable();
				
				// In addition to the fields we made
				// before, we are going to add a couple
				// of timestamp fields to our database.
				// Crud lets us automatically manage these
				// fields and they can come in handy.
				$table->integer('created_at');
				$table->integer('updated_at');
			});
	
			/* # Create Menu Items
			================================================== */
	
			// Create a menu item. Menu items are an instance of the
			// Platofrm\Menus\Menu model, which is an instand of Crud.
			// Create a new Book the same way you create any other Crud
			// model.
			$books = new Menu(array(
				'name'          => 'Books',
				'extension'     => 'books',
				'slug'          => 'admin-books-list',
				'uri'           => 'books',
				'user_editable' => 0,
				'status'        => 1,
			));
	
			// Find dashboard menu item
			$dashboard = Menu::find(function($query)
			{
				return $query->where('slug', '=', 'admin-dashboard');
			});
	
			// If there is no dashboard item for whatever
			// reason, we just simply insert our books item
			// as the last item in the administration menu, by
			// making it the 'last_child'
			if ($dashboard === null)
			{
				$admin = Menu::admin_menu();
				$books->last_child_of($admin);
			}
	
			else
			{
				// If we found the dashboard item, we're
				// going to make this Books item come right after
				// it, making it the 'next_sibling' of the Dashboard
				// item
				$books->next_sibling_of($dashboard);
			}
	
			/* # Configuration Settings
			================================================== */
	
		}
	
		/**
		 * Revert the changes to the database.
		 *
		 * @return void
		 */
		public function down()
		{
			// Remove the books table
			Schema::drop('books');
	
			// Remove the books item
			$books = Menu::find(function($query)
			{
				return $query->where('slug', '=', 'admin-books-list');
			});
	
			if ($books instanceof Books)
			{
				$books->delete();
			}
		}
	
	}



----------
