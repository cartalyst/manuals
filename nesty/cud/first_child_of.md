###first_child_of($parent)

---------

This method assigns an Nesty object to be the first child of the `$parent` parameter.

The function returns `integer` and throws `NestyException` only if the `$parent` does not exist.

#####Examples:

	try
	{
		// Get ford
		$ford = Model_Car::find(function($query)
		{
			return $query->where('name', '=', 'Ford');
		});

		$falcon = new Model_Car(array(
			'name' => 'Falcon',
		));

		/**
		 * Make falcon first child
		 * of Ford
		 */
		$falcon->first_child_of($ford);
	}
	catch (NestyException $e)
	{
		$error = $e->getMessage();
	}

#####Database Table:

  id        | name      | lft         | rgt         | tree_id
  :-------- | :-------- | :---------: | :---------: | :------:
  1         | Ford      | 1           | 4           | 1
  2         | Falcon    | 2           | 3           | 1


#####Nested Structure:

	Ford
	|   Falcon

---------