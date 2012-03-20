<a id="installation"></a>
##Installation

Once downloaded, you may want to add sentry to the always load packages array in 'app/config.php'. Installing the tables is as simple as running an oil migration.

>Notes: Your database connection needs to be setup first. The DB_Util code can be found in sentry/migrations if you can not install via oil for some reason. If you wish to change the default table names, you may adjust them in the configuration file.

    $ php oil r migrate --packages=sentry

##Special thanks to

_Contributin Authors John Doe, Henry Nutsack_
