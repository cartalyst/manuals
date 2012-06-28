###Update

----------

Updating works in the same way as creating, except you also need to pass the primary key value. When passing a primary key value, Crud will automatically assume that you want to update.

Of course, when you use any of the methods to find records (outlined in the **read** article), this is automatically done for you.

#####Examples

	// Create a user object with
	// a primary key (id) passed to it.
	// Crud knows we're updating
	$user = new User(array(
		'id'    => 5
		'email' => 'john.doe@update.com' // update the email
	));

	// Or
	$user = new User();
	$user->id    = 5,
	$user->email = 'john.doe@update.com';

	// Or
	$user = User::find(5);
	$user->email = 'john.doe@update.com';

	// Now save it
	$user->save();

----------
