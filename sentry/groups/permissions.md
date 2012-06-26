<a id="permissions" href="#"></a>
###permissions()

----------

Retrieves the groups permissions

`returns` array

####Example

	try
	{
		// get groups permissions
		$permissions = Sentry::user('admin')->permissions();
	}
	catch (SentryException $e)
	{
	    $errors = $e->getMessage(); // catch errors such as user does not exist.
	}
