###dump_as($format, $name = null, $type = 'nesty')

While this method is used primarily for debugging, it can be used instead of <kbd>get_children</kbd>	as a way of looping through children objects, although it is not as powerful as that method. This method currently supports dumping an object and / or it's children in the following formats:

1.  Array
2.  Unordered list
3.  Ordered list
4.  JSON string
5.  XML string
6.  Serialised PHP array
7.  PHP code (can be used with <a href="http://php.net/manual/en/function.eval.php" target="_blank">eval()</a> for example)

<table>
	<tr>
		<th>Parameters</th>
		<td><table class="parameters">
				<tr>
					<th>Param</th>
					<th>Type</th>
					<th>Default</th>
					<th>Description</th>
				</tr>
				<tr>
					<td><kbd>$format</kbd></td>
					<td>string</td>
					<td></td>
					<td>
						The format to dump in. Can be:
						<br>
						<kbd>array</kbd> | <kbd>ul</kbd> | <kbd>ol</kbd> | <kbd>json</kbd> | <kbd>xml</kbd> | <kbd>serialized</kbd> | <kbd>php</kbd>
					</td>
				</tr>
				<tr>
					<td><kbd>$name</kbd></td>
					<td>string</td>
					<td>null</td>
					<td>
						The name of the property to use for each dumped item. Defaults to the <a href="#configure-nesty-cols">name nesty column</a>. A closure can be provided as this parameter. The closure takes one parameter, the Nesty object that's being dumped at that point in time.
					</td>
				</tr>
				<tr>
					<td><kbd>$type</kbd></td>
					<td>string</td>
					<td>nesty</td>
					<td>
						The type of dumping we're doing. Either 'nesty' or 'children'. Nesty will dump the current nesty as the top level object and children as a sub-property of that object. Children will start the process with the children of the current Nesty and skip dumping it.
					</td>
				</tr>
			</table></td>
	</tr>
	<tr>
		<th>Returns</th>
		<td>mixed</td>
	</tr>
</table>

#####Examples:

	// Get ford
	$ford = Model_Car::find_one_by_name('Ford');

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

*   Ford
    *   Falcon
    *   F150
    *   Territory
        *   TX
    *   Festiva

	// Get ford
	$ford = Model_Car::find_one_by_name('Ford');

	// Dump ford
	$ford->dump_as('ol', function($nesty)
	{
		return sprintf('Car #%d: Name: %s',$nesty->id, $nesty->name);
	});

#####Outputs:

1.  Car #1: Name: Ford
    1.  Car #2: Name: Falcon
    2.  Car #4: Name: F150
    3.  Car #3: Name: Territory
        1.  Car #6: Name: TX
    4.  Car #5: Name: Festiva
