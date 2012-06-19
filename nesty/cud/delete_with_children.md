###delete_with_children()

-----------

This method returns an `integer`; the number of records affected.

>**Notes:** This method will delete a Nesty object and all of it's children objects (if they exist). See `delete()` if you do not want to delete children also.

#####Example:

	// Sorry Territory, you're gone!
	$territory = Model_Car::find(function($query)
	{
		return $query->where('name', '=', 'Territory');
	});
	
	$territory->delete();

#####Database Table:

id        | name      | lft         | rgt         | tree_id
:-------- | :-------- | :---------: | :---------: | :------:
1         | Ford      | 1           | 8           | 1
2         | Falcon    | 2           | 3           | 1
4         | F150      | 4           | 5           | 1
5         | Festiva   | 6           | 7           | 1


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

And we deleted the "Falcon" Nesty object. Our new structure would be:

	Ford
	|   F150
	|   Festiva

Note how "Falcon" and all it's children are gone.

----------
