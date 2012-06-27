###from_hierarchy_array($id, $items, $before_root_persist = null, $before_persist = null)

----------

This method takes a set of nested arrays that represent the tree structure and maps them to a Nesty tree.

Parameters                       | Type              | Default       | Description      
:------------------------------- | :-------------:   | :------------ | :---------------  
`$key`                           | int \| string     |               | Key of the root Nesty object the tree belongs to
`$items`                         | array             |               | An array of nested hierarchical items 
`$before_root_persist`           | Closure           | null          | Closure (`takes` Nesty root object, `returns` Nesty root object) to manipulate object before it's persisted to the database. Returning false means the changes to the root item aren't persisted.
`$before_item_persist`           | Closure           | null          | Closure (`takes` Nesty item object, `returns` Nesty item object) to manipulate object before it's persisted to the database. Returning false means the changes to the item item aren't persisted.

The function `returns` Nesty (root item in tree) and `throws` NestyException only if an invalid `$key` is provided for the root Nesty object (either doesn't exist or isn't a root object).

>**Notes:** Each item is represented as an array, with key / value properties representing database column names / values. For example:

	$item = array(
		'id'     => 2,
		'name'   => 'Foo',
		'slug'   => 'foo',
		'status' => 1,
	);

#####Database Table:

  id        | name      | slug        | status      | lft          | rgt          | tree_id
  :-------- | :-------- | :---------: | :---------: | :---------:  | :---------:  | :------:
  2         | Foo       | foo         | 1           | *Irrelevent* | *Irrelevent* | 1

If the primary key isn't provided, a new item will be persisted to the database when this method is invoked.

To nest children, you use a key / value declaration within an item, where `children` is the key, and the value is an array containing children items.

####Example

	$items = array(
		array(
			'id'   => 2,
			'name' => 'Holden',
		),
		array(
			'id'   => 3,
			'name' => 'Ford',
		),

		// Note, there is no primary key field here...
		// A new Nesty object will be created
		array(
			'name' => 'Toyota',
		),
	);

	$tree = Nesty::from_hierarchy_array(1, $items);

#####Database Table:

  id        | name      | lft         | rgt         | tree_id
  :-------- | :-------- | :---------: | :---------: | :------:
  1         | Cars      | 1           | 8           | 1
  2         | Holden    | 2           | 3           | 1
  3         | Ford      | 4           | 5           | 1
  4         | Toyota    | 6           | 7           | 1

####Example

	// Let's add to the previous setup
	$items = array(
		array(
			'id'   => 2,
			'name' => 'Holden',
		),
		array(
			'id'   => 3,
			'name' => 'Ford',
		),

		array(
			'name' => 'Toyota',

			// Nest children within this reserved
			// key name
			'children' => array(

				array(
					'name' => 'Prius',
				),
				array(
					'name' => 'Camry',
				),
				array(
					'name' => 'Celica',
				),
				array(
					'name' => 'Hilux',
				),

			),
		),
	);

	$tree = Nesty::from_hierarchy_array(1, $items);

#####Database Table:

  id        | name      | lft         | rgt         | tree_id
  :-------- | :-------- | :---------: | :---------: | :------:
  1         | Cars      | 1           | 16          | 1
  2         | Holden    | 2           | 3           | 1
  3         | Ford      | 4           | 5           | 1
  4         | Toyota    | 6           | 15          | 1
  5         | Prius     | 7           | 8           | 1
  6         | Camry     | 9           | 10          | 1
  7         | Celica    | 11          | 12          | 1
  8         | Hilux     | 13          | 14          | 1

>**Notes:** `from_hierarchy_array()` maps the provided array with the database. This means if you don't provide an entry in the mapped array that exists in the database, it will be deleted from the database. Be wary of this.

####Example

	// Let's add to the previous setup
	$items = array(
		array(
			'id'   => 2,
			'name' => 'Holden',
		),
		array(
			'id'   => 3,
			'name' => 'Ford',
		),

		array(
			'name' => 'Toyota',

			// Nest children within this reserved
			// key name
			'children' => array(

				array(
					'name' => 'Prius',
				),
				array(
					'name' => 'Camry',
				),
				array(
					'name' => 'Celica',
				),
				array(
					'name' => 'Hilux',
				),

			),
		),
	);

	// Let's manipulate the items before they're inserted in
	// the databse. The power of this is endless
	$tree = Nesty::from_hierarchy_array(1, $items, function($root_item)
	{
		// Prepend text
		$root_item->name = 'Foo '.$root_item->name;
		return $root_item;

	}), function($item)
	{
		// No Prius in table
		if ($item->name == 'Prius')
		{
			return false;
		}

		$item->name = 'Bar '.$item->name;
		return $item;
	});

#####Database Table:

  id        | name        | lft         | rgt         | tree_id
  :-------- | :--------   | :---------: | :---------: | :------:
  1         | Foo Cars    | 1           | 14          | 1
  2         | Bar Holden  | 2           | 3           | 1
  3         | Bar Ford    | 4           | 5           | 1
  4         | Bar Toyota  | 6           | 13          | 1
  6         | Bar Camry   | 7           | 8           | 1
  7         | Bar Celica  | 9           | 10          | 1
  8         | Bar Hilux   | 11          | 12          | 1

----------
