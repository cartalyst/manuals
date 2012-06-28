###Delete

----------

Deleting a model is as simple as calling delete on an existing Crud model that contains a key.

>**Notes:** If you try to delete a model and no primary key is set, an exception will be thrown.

#####Examples

	// Create a user with a
	// primary key that matches the
	// database
	$user = new User(array(
		'id' => 5
	));

	// Or
	$user = User::find(5);

	// Delete
	$user->delete();

	// Find all users who's
	// first name is Ben
	$users = Users::all(function($query)
	{
		return $query->where('first_name', '=', 'Ben');
	});

	// Loop through and delete
	foreach ($users as $user)
	{
		$user->delete();
	}

----------
