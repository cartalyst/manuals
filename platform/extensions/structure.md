###Structure

----------

Here is an example folder structure for an Extension. We'll use Users for our example. Note that most of the structure is optional depending on what you want to do with your extension.  The only non-optional item is the new extension.php file.

###Vendors

----------

A new feature to Platform 1.1 is vendor separation of extensions. This means that you can have multiple extensions named the same, from different vendors. Additionally, we have added functionality to extend and override functionality of a core extension (or another third party extension) with ease.

----------

* vendor_name
	* extension_name
		* controllers
			* admin *( new )*
				* admin controllers
			* api *( new )*
				* api controllers
		* configuration
		* language
		* migrations
		* models
		* plugins *( new )*
		* widgets *( new )*
		* extension.php *( new | required )*
		* routes.php
		* start.php
