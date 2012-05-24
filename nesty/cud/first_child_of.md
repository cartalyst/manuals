###first_child_of(Nesty &amp;$parent)

---------

Assigns a Nesty object to a parent Nesty object.

**Parameters:**

  Parameter  | Type      | Default     | Description
  :--------- | :-------- | :---------: | :----------: |
  $parent    | Nesty     |             | An instance of a Nesty Object to be the first child of. |

**Returns:** 
Int

**Throws:** 
NestyException


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
