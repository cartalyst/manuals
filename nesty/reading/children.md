###children($limit = false)

----------

The `children` method returns an `array` of children Nesty objects for the Nesty object on which this method was called.


> <strong>**Notes:**</strong>	This method alone demonstrates one of the best features of the <strong>modified preorder tree traversal algorithm</strong> (the nested sets pattern Nesty uses). We can recursively grab every single child Nesty using the one database query! What does this mean? It's super fast!

> Typically, you would normally call `children()` with no parameters, which will recursively nest children objects within this object. That way, every `children()` call on child objects doesn't require a second database call - because they've already been fetched!

> The only reason you wouldn limit the depth of children found is when you know that you will not be going any deeper down the hierarchy tree. This is to simply save on memory usage and the time taken to hydrate the children property of each Nesty object recursively.


Parameters                   | Type            | Default       | Description      
:--------------------------- | :-------------: | :------------ | :---------------  
`$limit`                     | string          | false         | The depth limit of children to hydrate. `false` (default) returns all children.
`$columns`                   | array           | array('*')    | Array of columns to select for children. Defaults to all columns.


###Examples:

	// Get ford
	$ford = Model_Car::find(function($query)
	{
		return $query->where('name', '=', 'Ford')
	});

	// Print children objects
	print_r($ford->children());

	/**
	 * The aboove line outputs the array
	 * below.
	 *
	 * Note, this array has been truncated
	 * just for demonstation purposes.
	 *
	 * Additionally, if the person called
	 * $ford->children(1), it would
	 * limit the recursion level to not
	 * show the children array of the
	 * 'Territory' model below.
	 */
	Array
	(
		...

	    [2] => Tags\Model\Car Object
	        (
	            [children] => Array
	                (
	                    [0] => Tags\Model\Car Object
	                        (
	                            [children] =>
	                            [_is_new:protected] =>
	                            [_is_frozen:protected] =>
	                            [_validation:protected] =>
	                            [_iterable:protected] => Array
	                                (
	                                )

	                            [id] => 6
	                            [name] => TX
	                            [lft] => 7
	                            [rgt] => 8
	                            [tree_id] => 1
	                            [depth] => 2
	                        )

	                )

	            [_is_new:protected] =>
	            [_is_frozen:protected] =>
	            [_validation:protected] =>
	            [_iterable:protected] => Array
	                (
	                )

	            [id] => 3
	            [name] => Territory
	            [lft] => 6
	            [rgt] => 9
	            [tree_id] => 1
	            [depth] => 1
	        )

	    ...
	)

----------
