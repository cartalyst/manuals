###last_child_of(Nesty &amp;$parent)

----------

This method returns the Nesty object.

<table>
	<tr>
		<th>Parameters</th>
		<td>
			<table class="parameters">
				<tr>
					<th>Param</th>
					<th>Type</th>
					<th>Default</th>
					<th>Description</th>
				</tr>
				<tr>
					<td>`$parent`</td>
					<td>Nesty</td>
					<td></td>
					<td>An instance of a Nesty object for which you want this object to be the last child of.</td>
				</tr>
			</table>
		</td>
	</tr>
	<tr>
		<th>Returns</th>
		<td>Nesty</td>
	</tr>
	<tr>
		<th>Throws</th>
		<td>NestyException</td>
	</tr>
</table>

#####Examples:

	try
	{
		// Get ford
		$ford = Model_Car::find(function($query)
		{
			return $query->where('name', '=', 'Ford');
		});

		$territory = Model_Car::forge(array(
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
