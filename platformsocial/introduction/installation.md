###Installation

----------

Once you have Platform Social downloaded, you will want to move the files into your platform directory. The directory layout will match an unmodified Platform setup for easy drag and drop installation.  You will also need to add the following line to your `application/bundles.php` file to load and run sentry social.

	'sentrysocial' => array('auto' => true),

Once your files are uploaded, log into your admin and go to `system > extensions`. Find Social in the uninstalled extension section and press install.

>**Note:** If you are testing on your localhost, you may need to enable the php setting `php_openssl` and possibly apache's `ssl_module` for OAuth2 in it's current state.
