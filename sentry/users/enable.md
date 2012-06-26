<a id="enable" href="#"></a>
###enable()

----------

Enables a user.

`returns` bool `throws` SentryException

####Example

	try
	{
	    $enabled = Sentry::user(25)->enable();
	    if ($enabled)
	    {
	        // user was enabled
	    }
	    else
	    {
	        // something went wrong
	    }
	}
	catch (SentryException $e)
	{
	    $errors = $e->getMessage();
	}
