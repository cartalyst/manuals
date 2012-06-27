###root()

----------

The `root` method returns the Nesty object.

The function returns `Nesty` and throws `NestyException`.

#####Examples:

	// Create a new car make
	try
	{
		$ford = new Model_Car(array(
			'name' => 'Ford',
		));

		/**
		 * Make Ford a new root
		 * Nesty object
		 */
		$ford->root();
	}
	catch (NestyException $e)
	{
		$error = $e->getMessage();
	}

#####Database Table:

  id        | name      | lft         | rgt         | tree_id
  :-------- | :-------- | :---------: | :---------: | :------:
  1         | Ford      | 1           | 2           | 1


#####Nested Structure:

	Ford

----------
