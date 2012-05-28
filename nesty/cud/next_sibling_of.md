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
		<td>10</td>
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
		<td>6</td>
		<td>7</td>
		<td>1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>F150</td>
		<td>4</td>
		<td>5</td>
		<td>1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>Festiva</td>
		<td>8</td>
		<td>9</td>
		<td>1</td>
	</tr>
</table>

#####Nested Structure:

	Ford
	|   Falcon
	|   F150
	|   Territory
	|   Festiva

----------
