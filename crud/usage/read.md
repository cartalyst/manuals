###Read

----------

There are a few ways to retrieve data using Crud. Crud supports:

 - Finding one record
 - Finding multiple records
 - Counting records
 - Counting distinct records

####Finding One Record

To find a specific model / record, use the `find()` method. This method takes two parameters, a `$condition` (to filter what records we want to find) and `$columns`; an array of columns to select.

	public function find($condition = 'first', $columns = array('*'))

The condition can be:

 - 'first' - find the first record in the table (sorted by primary key).
 - 'last' - find the last record in the table (sorted by primary key).
 - Value - of primary key to find one record by
 - Closure - accepts a `$query` object and returns the modified `$query` object.

#####Examples

	// Find the first record in the table
	$user = User::find('first');

	// Find the last record in the table
	$user = User::find('last', array('id', 'first_name'));

	// Find all columns where the users primary key is equal to 5
	$user = User::find(5);

	// Finds the users first and last where the primary key is equal to 3
	$user = User::find(3, array('first_name', 'last_name'));

	// Find the first user who's name is Ben
	$user = User::find(function($query)
	{
		return $query->where('first_name', '=', 'Ben');
	});

	// Find the first user who's last name is Petrie, selecting
	// only the first name
	$user = User::find(function($query)
	{
		return $query->where('last_name', '=', 'Petrie');
	}, array('first_name'));

####Finding All Records

If you wish to retrieve all models / records in the table, you can use the `all()` method. Like `find()`, this accepts two parameters, `$condition` and `$columns`.

#####Examples

	// Find all users who's first name starts with 'b'
	$users = User::all(function($query)
	{
		return $query->where('first_name', 'LIKE', 'b%');
	});

	// Find all active users, selecting just their id
	$users = User::all(function($query)
	{
		return $query->where('active', '=', 1);
	}, array('id'));

####Counting Records

To count records, call `count()`. This accepts two parameters, the `$column` to count by and a `$condition` to manipulate the query.

	public function count($column = null, $condition = null)

>**Notes:** The columnn will default to the primary `$_key`.

#####Examples

	// Count users
	$count = Users::count('id');

	// Count users who's last name contains a 'p'
	$count = Users::count('id', function($query)
	{
		return $query->where('last_name', 'LIKE', '%p%');
	});

####Counting Disting Records

To count distinct records, call `count_distinct()`. This method, like `count()`, excepts both `$column` and `$condition`.

####Examples

	// Count unique first name's in the `users` table.
	$count = Users::count_distinct('first_name');

----------
