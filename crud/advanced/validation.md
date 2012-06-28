###Rules and Validation

----------

To set validation rules, set this property to a array of validation rules normally.  Crud will automatically run the validation and return false if it fails.

	protected static $_rules = array(
		'first_name' => 'required',
		'last_name'  => 'required',
		'email'      => 'required|email'
	)

If validation fails, you would probably want to retrieve the validation object so you can set error messages.  Well to do this, you just need to call the validation method.

	// Save our user
	$success = $user->save();

	if ( ! $success)
	{
		// Get the validation object
		$validation = $user->validation();

		// $validation is a Validation instance. All
		// Validation methods are available.
		$errors = $validation->errors->all();
	}

----------
