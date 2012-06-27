###previous_sibling_of($sibling)

----------

This method assigns an Nesty object for which you want this object to be the previous `$sibling` of.

The function returns `Nesty` and throws `NestyException` only if the `$sibling` does not exist.

#####Examples:

	try
	{
		$territory = Model_Car::find(function($query)
		{
			return $query->where('name', '=', 'Territory');
		});

		$f150 = new Model_Car(array(
			'name' => 'F150',
		));

		/**
		 * Make previous
		 * sibling of the Territory
		 */
		$f150->previous_sibling_of($territory);
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
  3         | Territory | 6           | 7           | 1
  3         | F150      | 4           | 5           | 1

#####Nested Structure:
	Ford
	|   Falcon
	|   F150
	|   Territory

----------
