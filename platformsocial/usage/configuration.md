###Configuration & Usage

----------

To use Platform Social is as easy as setting your providers credentials in a configuration file and calling a widget.

#### Providers

First, you will need to find the developer area of the provider you wish to add and create a new OAuth(2) application.  When creating this application, they will typically ask you for a callback url.  Set this to `http://yourdomain.com/social/social/callback/{provider}`. Here is an example callback url for Twitter: `http://yourdomain.com/social/social/callback/twitter`

Once the application is created, make sure to find the `app id` and `app secret` codes as you will need them later on.  These may be named differently from provider to provider.

Once you have your codes, open up `platform/bundles/sentrysocial/config/sentrysocial.php` and add your provider and keys to the file. Provider options consist of application id and secret for OAuth, add in scope for OAuth2 and the type of authentication to use between OAuth and OAuth2. All the other

Example for both OAuth and OAuth2 configurations are listed below

	return array(

		/**
		 * Social Providers
		 */
		'providers' => array(

			'twitter' => array(
				'app_id'     => 'your app id',
				'app_secret' => 'your app secrete',
				'driver'     => 'OAuth',
			),

			'facebook' => array(
				'app_id'     => 'your app id',
				'app_secret' => 'your app secret',
				'scope'      => array('offline_access'),
				'driver'     => 'OAuth2'
			),
		)
	);

Once a provider is listed, the widget will add it to be displayed automatically along with a standard login form. Currently it will add a `jpg` image from the `social/assets/img` folder with the same name as the provider.  So if you want a twitter image, add a `twitter.jpg` image to this folder.

#### Widget

Once you are done configuring your providers, you just need to make a widget call to display the social login form wherever you want it.  Simply make the following call and you are all done!

	@widget('cartalyst/social::form.login')