###delete()

-----------

This method returns an integer; the number of records affected.

&gt; **Notes:** Be warned, this method will remove all children Nesty objects of the object that `delete()` is called on. In future versions we are planning to add the ability assign orphaned children to the parent of this deleted object (they will move up one level).

Returns                          | Throws 
:------------------------------- | :-------------
Int                              | 


#####Example:

	// Sorry Territory, you're gone!
	$territory = Model_Car::find_one_by_name('Territory');
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

And we deleted the "FPV" Nesty object. Our new structure would be:

	Ford
	|   Falcon
	|   |   Futura
	|   F150
	|   Festiva

Note how the children Nesty objects of FPV have also disappeared from the database.
