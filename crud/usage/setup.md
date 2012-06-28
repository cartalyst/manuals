###Setup

----------

To begin using Crud, we need to setup a barebones model. Create a file called `user.php` and place it in the **models** directory of your laravel installation's **application** path.

	class User extends Crud
	{

		protected static $_key = 'id';

		protected static $_table = 'users';

	}

By default, Crud will set your primary `$_key` to 'id' and your `$_table_name` to the plural form of the class name via Laravels `Str::plural()`. If you wish to have a different primary key or table, all you need to to do is override a couple of properties.

Because of this, you can set up your Users model as such:

	class User extends Crud
	{

	}

----------
