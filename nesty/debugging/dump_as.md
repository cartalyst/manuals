###dump_as($format, $name, $type = 'nesty')

----------

Depending on the format provided, this method returns a variety of data types. While this method is used primarily for debugging, it can be used instead of `children` as a way of iterating through children objects, although it is not as powerful as `children`.

Returns                          | Throws 
:------------------------------- | :-------------
string \| array                  | NestyException


Parameters                       | Type              | Default       | Description      
:------------------------------- | :-------------:   | :------------ | :---------------  
`$format`                        | string            |               | Format to dump as (see below)
`$name`                          | string \| Closure | null          | Name of each object when it's dumped. Defaults to the `name` nesty column defined in your **configuration**. Alternatively, a closure may be provided which takes the Nesty object as it's parameter and must return a string for the `name`.
`$type`                          | string            | nesty         | The type of dump to performm. Either `nesty` or `children`. Nesty will dump the object that `dump_as` is called on as well as it's children, `children` will dump the children only.

This method currently supports dumping an object and / or it's children in the following formats:

Format     | Description
:--------- | :---------------------------------
array      | An array containing dumped objects
ul         | Unordered list `<ul>`
ol         | Ordered list `<ol>`
json       | JSON string
serialized | Serialized PHP array
php        | String representing PHP code - could use with [`eval()`](http://php.net/manual/en/function.eval.php)


####Example 1:

	// Get ford
	$ford = Model_Car::find(function($query)
	{
		return $query->where('name', '=', 'Ford');
	});

	// Dump ford
	$ford->dump_as('array');

	/*
	Outputs:

	    Array
	    (
	        [Ford] => Array
	            (
	                [0] => Falcon
	                [1] => F150
	                [Territory] => Array
	                    (
	                        [0] => TX
	                    )

	                [2] => Festiva
	            )

	    )
	*/

	// Get ford
	$ford = Model_Car::find_one_by_name('Ford');

	// Dump ford
	$ford->dump_as('ul');

#####Outputs:

* Ford
  * Falcon
  * F150
  * Territory
    * TX
  * Festiva

####Example 2:

	// Get ford
	$ford = Model_Car::find(function($query)
	{
		return $query->where('name', '=', 'Ford');	
	});

	// Dump ford
	$ford->dump_as('ol', function($nesty)
	{
		return sprintf('Car #%d: Name: %s',$nesty->id, $nesty->name);
	});

#####Outputs:

1. Car #1: Name: Ford
   1. Car #2: Name: Falcon
   2. Car #4: Name: F150
   3. Car #3: Name: Territory
      1. Car #6: Name: TX
   4. Car #5: Name: Festiva

----------
