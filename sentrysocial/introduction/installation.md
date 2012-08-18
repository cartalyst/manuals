###Installation

----------

Once you have SentrySocial downloaded, you will want to put all the `sentrysocial` folder in your bundles folder.  Then you will want to add the following lines to your `application/bundles.php` file to load and run sentry social.

	'sentrysocial' => array(
		'auto'     => true,
		'handles'  => 'sentrysocial'
	),

Installing the table for SentrySocial is as simple as running its migration.

	php artisan migrate sentrysocial

>**Note:** If you do not want to use the default controller, you can remove `handles` from bundles.php and copy or extend it elsewhere.  This is just a working example controller.
