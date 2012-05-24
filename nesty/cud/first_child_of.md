###first_child_of($parent)

---------

This method assigns an Nesty object to be the first child of the `$parent` parameter.

`first_child_of($parent);` Returns Int, Throws NestyException


#####Examples:

	try
	{
		// Get Parent
		$ford = Model_Car::where('name', '=', 'Ford')->get();

		$falcon = new Model_Car(array(
			'name' => 'Falcon',
		));

		/**
		 * Make first child
		 * of Ford
		 */
		$ford->first_child_of($ford);
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


#####Nested Structure:

	Ford
	|   Falcon
