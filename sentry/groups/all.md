<a id="all" href="#"></a>
###all()

----------

The all method returns all groups

`returns` array `throws` SentryException

####Example

	// get group information
	try
	{
	    $groups = Sentry::group()->all();
	}
	catch (SentryGroupException $e)
	{
	    $errors = $e->getMessage();
	}
