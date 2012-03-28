###delete()

-----------

This method returns an integer; the number of records affected.

> <strong>Notes:</strong> Be warned, this method will remove all children Nesty objects of the object that <kbd>delete()</kbd> is called on. In future versions we are planning to add the ability assign orphaned children to the parent of this deleted object (they will move up one level).

<table>
	<tr>
		<th>Returns</th>
		<td>Int</td>
	</tr>
</table>

#####Example:

	// Sorry Territory, you're gone!
	$territory = Model_Car::find_one_by_name('Territory');
	$territory->delete();

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
		<td>8</td>
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
		<td>4</td>
		<td>F150</td>
		<td>4</td>
		<td>5</td>
		<td>1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>Festiva</td>
		<td>6</td>
		<td>7</td>
		<td>1</td>
	</tr>
</table>

#####Nested Structure:

	Ford
	|   Falcon
	|   F150
	|   Festiva

#####Example:

Say we had the following Nested Structure:

	Ford
	|   Falcon
	|   |   Futura
	|   |   FPV
	|   |   |   GT
	|   |   |   F6
	|   |   |   GS
	|   F150
	|   Festiva

And we deleted the "FPV" Nesty object. Our new structure would be:

	Ford
	|   Falcon
	|   |   Futura
	|   F150
	|   Festiva

Note how the children Nesty objects of FPV have also disappeared from the database.
