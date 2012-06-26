### About

----------

The logs extensions allows you to easily view and filter actions users have made in the admin section of your site.  It shows who made the action, when, what extension the action was done in and a message of the event that was fired.  This message is dynamically created from the events key name with an id of the record that was modified if available.

> **Note:** Logs will only be stored for extensions that have their events registered in the `events` section of their `extension.php` file.  Those events have to exist for Logs to listen to them.
