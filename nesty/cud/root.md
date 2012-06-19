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
		<td>2</td>
		<td>1</td>
	</tr>
</table>

#####Nested Structure:

	Ford

----------
