<a id="create" href="#"></a>
###create($group)

----------

The create method creates a new group.

Parameters                   | Type            | Default       | Description
:--------------------------- | :-------------: | :------------ | :--------------
`$group`                     | array           |               | An array of consisting of the groups 'name' and 'level'. Optional fields are 'is_admin' and 'parent'. The group name must be unique.

`returns` bool, int - false or group id `throws` Sentry\SentryException

####Example

	// create a group
	try
	{
	    $group_id = Sentry::group()->create(array(
	        'name'  => 'myadmin',
	        'level' => 100,
	    ));
	}
	catch (Sentry\SentryException $e)
	{
	    $errors = $e->getMessage();
	}
