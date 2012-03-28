###Nesty Columns

----------

<kbd>protected static $_nesty_cols</kbd> contains 4 properties. You can choose to customise these properties in this array and your table, should do wish to do so.

<table>
	<tr>
		<th>Option</th>
		<th>Type</th>
		<th>Default</th>
		<th>Description</th>
	</tr>
	<tr>
		<td>left</td>
		<td>string</td>
		<td>lft</td>
		<td>The left-hand identifier for a Nesty object</td>
	</tr>
	<tr>
		<td>right</td>
		<td>string</td>
		<td>rgt</td>
		<td>The right-hand identifier for a Nesty object</td>
	</tr>
	<tr>
		<td>name</td>
		<td>string</td>
		<td>name</td>
		<td>The name property for a Nesty object. Typically used for the label of a Nesty object when displaying</td>
	</tr>
	<tr>
		<td>tree</td>
		<td>string</td>
		<td>tree_id</td>
		<td>The tree identifier for a Nesty object (Nesty supports multiple trees in the one table)</td>
	</tr>
</table>

#####Example of a typical Nesty Model:

	class Model_Car extends Nesty
	{
		// Set the table name
		protected static $_table_name = 'cars';
	}

#####Slightly more configured Nesty Model:

	class Model_Car extends Nesty
	{
		// Set the table name
		protected static $_table_name = 'cars';

		// Sets the rules
		protected static $_rules = array(
			'name' => 'required',
		);

		// Set labels for our rules
		protected static $_lables = array(
			'name' => 'Name field',
		);

		/**
		 * Override the nesty cols in the
		 * database
		 */
		protected static $_nesty_cols = array(
			'left'  => 'left_limit',
			'right' => 'right_limit',
			'name'  => 'label',
			'tree'  => 'tree_id',
		);
	}
