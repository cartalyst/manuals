###Other Methods

----------

There are other methods available to Crud. What better way, than to show you in action?

#####Examples

	// Load a new model
	$model = new Crud();

	// Array of key / value attribute pairs
	$attributes = array(
		'first_name' => 'Ben',
		'last_name'  => 'Corlett',
	);

	// Fill a model with attributes
	$model->fill($attributes);

	// Return the attributes for the model
	$model->attributes();

	// Return the validation object
	// If one exists
	$model->validation();

	// Set if a model is new or not
	$model->is_new($bool);

	// Find out if model is new
	$model->is_new();

	// Find the table name for a model
	User::table();

----------
