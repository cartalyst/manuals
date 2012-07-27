### Usage

----------

Logs is extremely simple to use.  To find logs, once installed, go to `System > Logs`. This should bring you to a table of event logs from the time the extension was installed.  The tables sorting and filters will work the same way it does with other tables native to platform.

----------

#### Registering Events

If you wish to log additional events, you just need to make sure that the events are listed in the extension.php file.  Logs will go through each registered extension.php file and find the listed events.  For the events that it finds, it will add an event listener to generate the log.

**example extension.php file**

	'events' => array(
		'user.create',
		'user.update',
		'user.delete',
		'group.create',
		'group.update',
		'group.delete',
	),