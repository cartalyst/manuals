###Authenticate

----------

Once you have installed and setup the configuration for SentrySocial, authentication is easy.  All you need to do is redirect the user to a specific url with the provider name as a paramater.

With our example controller, you would just need to redirect the user to `sentrysocial/auth/session/provider` where provider is who you want to authenticate through.  So for twitter your redirect would read `sentrysocial/auth/session/twitter`.  From here, the user will be prompted to grant access to your app for authentication.