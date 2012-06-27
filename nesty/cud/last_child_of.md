###last_child_of($parent)

----------

This method assigns an Nesty object to be the last child of the `$parent` parameter.

The function returns `integer` and throws `NestyException` only if the `$parent` does not exist.

#####Examples:

	try
	{
		// Get ford
		$ford = Model_Car::find(function($query)
		{
			return $query->where('name', '=', 'Ford');
		});

		$territory = new Model_Car(array(
			'name' => 'Territory',
		));

		/**
		 * This will be put as the new
		 * last child of Ford
		 */
		$territory->last_child_of($ford);
	}
	catch (NestyException $e)
	{
		$error = $e->getMessage();
	}

#####Database Table:

  id        | name      | lft         | rgt         | tree_id
  :-------- | :-------- | :---------: | :---------: | :------:
  1         | Ford      | 1           | 8           | 1
  2         | Falcon    | 2           | 3           | 1
  3         | Territory | 4           | 5           | 1

#####Nested Structure:

	Ford
	|   Falcon
	|   Territory

----------
