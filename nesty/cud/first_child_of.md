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
		$ford = Model_Car::find_one_by_name('Ford');

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
		<td>4</td>
		<td>1</td>
	</tr>
	<tr>
		<td>2</td>
		<td>Falcon</td>
		<td>2</td>
		<td>3</td>
		<td>1</td>
	</tr>
</table>

#####Nested Structure:

	Ford
	|   Falcon
