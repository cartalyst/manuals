###next_sibling_of($sibling)

----------

This method assigns an Nesty object for which you want this object to be the next `$sibling` of.

The function returns `Nesty` and throws `NestyException` only if the `$sibling` does not exist.

#####Examples:

	try
	{
		$territory = Model_Car::find(function($query)
		{
			return $query->where('name', '=', 'Territory');
		});

		$festiva = new Model_Car(array(
			'name' => 'Festiva',
		));

		/**
		 * Make previous
		 * sibling of the Territory
		 */
		$festiva->next_sibling_of($territory);
	}
	catch (NestyException $e)
	{
		$error = $e->getMessage();
	}


#####Database Table:

  id        | name      | lft         | rgt         | tree_id
  :-------- | :-------- | :---------: | :---------: | :------:
  1         | Ford      | 1           | 10          | 1
  2         | Falcon    | 2           | 3           | 1
  3         | Territory | 6           | 7           | 1
  3         | F150      | 4           | 5           | 1
  3         | Festiva   | 8           | 9           | 1

#####Nested Structure:

	Ford
	|   Falcon
	|   F150
	|   Territory
	|   Festiva

----------
