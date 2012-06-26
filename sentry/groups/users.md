<a id="users" href="#"></a>
###users()

----------

The users method returns all the users in the group.

`returns` array `throws` SentryException

####Example

	// get group information
	try
	{
	    $users = Sentry::group(2)->users();
	}
	catch (SentryGroupException $e)
	{
	    $errors = $e->getMessage();
	}
