###Configuration

----------

Before you try to authenticate a user with SentrySocial, you need to set some configuration options first.

#### Callback URL

The callback url is used to set a url relative to your domain that services can point back to for continued authentication processing. With our example controller used in sentry social, this configuration option is set to `sentrysocial/auth/callback`.

Another key point to this config option is that it needs to match the url you put in your providers application callback url with one exception. This exception is that you need to add the providers name to the end of the url.

What does this mean? We'll use facebook for an example.  In your facebook app settings, you need to set your site url to `yourdomain.com/sentrysocial/auth/callback/facebook`.  This is simply your full configuration path plus the provider name.

#### Providers

The other configuration options you need to set are for your social authentication providers.  These configuration options consist of application id and secret for OAuth , add in scope for OAuth2 and the type of authentication to use between OAuth and OAuth2.

Example for both OAuth and OAuth2 configurations are listed below


	return array(

		/**
		 * Callback URL
		 */
		'callback_url' => 'sentrysocial/auth/callback',

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