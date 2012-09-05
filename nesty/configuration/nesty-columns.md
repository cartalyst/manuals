###Nesty Columns

----------

`protected static $_nesty_cols` contains 4 properties. You can choose to customise these properties in this array and your table, should do wish to do so.

Option                       | Type            | Default       | Description      
:--------------------------- | :-------------: | :------------ | :---------------  
left                         | string          | lft           | The left-hand identifier for a Nesty object
right                        | string          | rgt           | The right-hand identifier for a Nesty object
name                         | string          | name          | The name property for a Nesty object. Typically used for the label of a Nesty object when displaying.
tree                         | string          | tree_id       | The tree identifier for a Nesty object. (Nesty supports multiple trees in one table) 


#####Example of a typical Nesty Model:

	class Model_Car extends Nesty
	{
		// Set the table name
		protected static $_table = 'cars';
	}

#####Slightly more configured Nesty Model:

	class Model_Car extends Nesty
	{
		// Set the table name
		protected static $_table = 'cars';

		// Sets the rules
		protected static $_rules = array(
			'name' => 'required',
		);

		// Set labels for our rules
		protected static $_labels = array(
			'name' => 'Name field',
		);

		/**
		 * Override the nesty cols in the
		 * database. If you override this property
		 * you must specify all four keys (left, right,
		 * name and tree). The defaults are provided
		 * in the comments.
		 */
		protected static $_nesty_cols = array(
			'left'  => 'left_limit',   // Default is `lft`
			'right' => 'right_limit',  // Default is `rgt`
			'tree'  => 'car_range_id', // Default is `tree_id`
		);
	}

----------
