###first_child_of(Nesty &amp;$parent)

---------

This method returns the Nesty object.

Returns                          | Throws 
:------------------------------- | :-------------
Int                              | NestyException

Parameters                       | Type            | Default       | Description      
:------------------------------- | :-------------: | :------------ | :---------------  
`$parent`                        | Nesty           |               | An instance of a Nesty object for which you want this object to be the first child of.


#####Examples:

	try
	{
		// Get ford
		$ford = Model_Car::find(function($query)
		{
			return $query->where('name', '=', 'Ford');
		});

		$falcon = Model_Car::forge(array(
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
