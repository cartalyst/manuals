###reload()

----------

This method returns the Nesty object.

The function returns `Nesty` and throws `NestyException`.

> <strong>**Notes:**</strong> If you are moving or inserting more than one Nesty object in a request, you should be calling `>reload()` on active Nesty objects. This is because, to achieve maximum speed for the user, Nesty updates the database using `UPDATE` queries. These do not automatically update the models that have been initialised. Calling `reload()` automatically updates the model's properties to reflect any database changes.

#####Examples:

	// Find the Ford Territory
	$territory = Model_Car::find(function($query)
	{
		return $query->where('name', '=', 'Territory');
	});

	/**
	 * Add a child ($t4)...
	 */
	$territory->reload();

	/**
	 * Add a child to $t4...
	 */
	$territory->reload();

	/**
	 * Etc...
	 */

----------
