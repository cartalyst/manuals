<a id="get" href="#"></a>
###get($field = null)

----------

The update method updates the current group.

Parameters                   | Type            | Default       | Description
:--------------------------- | :-------------: | :------------ | :--------------
`$field`                     | string, array   | null          | The name or names of fields to retrieve.

`returns` string, array `throws` SentryException

####Example

	// get group information
	try
	{
	    $group_level = Sentry::group(2)->get('level');
	    //or
	    $group_info = Sentry::group(2)->get(array('name', 'level'));
	    //or
	    $group_info = Sentry::group(2)->get();
	}
	catch (SentryGroupException $e)
	{
	    $errors = $e->getMessage();
	}
