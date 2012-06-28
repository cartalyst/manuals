###Setup

----------

To create a user, all you need to do is instantiate a new instance of the model with the data you wish to add and save it.

>**Notes:** If you provide a primary key to a record that's not in the database, an error will occur when you attempt to persist the model. This is because Crud assumes that if a primary key is present, you are updating an existing record. If you manually passing a primary key, you need to set the model to new, by setting the second parameter of the construct (`new User()`) to 'true'. Alternatively, you can call `is_new()` on an object instance.

#####Examples

	// Create a user object
	$user = new User(array(
		'first_name' => 'John',
		'last_name'  => 'Doe',
		'email'      => 'john.doe@crud.com'
	));

	// Or
	$user = new User();
	$user->first_name = 'John',
	$user->last_name  = 'Doe',
	$user->email      = 'john.doe@crud.com';

	// Or when passing a primary key
	$user = new User(array(
		'id'         => 10
		'first_name' => 'John',
		'last_name'  => 'Doe',
		'email'      => 'john.doe@crud.com'
	), true);

	// Or
	$user = new User();
	$user->id         = 10
	$user->first_name = 'John',
	$user->last_name  = 'Doe',
	$user->email      = 'john.doe@crud.com';
	$user->is_new(true);

	// Now save it
	$user->save();

----------
