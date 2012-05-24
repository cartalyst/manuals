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

<table>
	<tr>
		<th>`id`</th>
		<th>`name`</th>
		<th>`lft`</th>
		<th>`rgt`</th>
		<th>`tree_id`</th>
	</tr>
	<tr>
		<td>1</td>
		<td>Ford</td>
		<td>1</td>
		<td>6</td>
		<td>1</td>
	</tr>
	<tr>
		<td>2</td>
		<td>Falcon</td>
		<td>2</td>
		<td>3</td>
		<td>1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>Territory</td>
		<td>4</td>
		<td>5</td>
		<td>1</td>
	</tr>
</table>

#####Nested Structure:

	Ford
	|   Falcon
	|   Territory
