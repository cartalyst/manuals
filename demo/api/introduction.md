###Introduction

----------

Platform at it's core is an API-driven platform^PunIntended. Everything in Platform interacts through an internal [REST-like](http://en.wikipedia.org/wiki/Representational_state_transfer) API. This allows extensions to be de-coupled as they do not need to interact directly with each other's models and classes, but rather the API can return data in standard formats (arrays / JSON). The data is sent from API controllers which respond to a particular URI route which is all controlled by the developer.

De-coupling is a fancy word that essentially means that extensions operate on their own and aren't dramatically affected by the existence / non-existence of other extensions. This is the only way to be truly modular.

In Platform, our extensions are de-coupled because:

- There are no references to direct classes. No more `class doesn't exist` errors if an extension is disabled or overridden.
- Because the API responds to URI routes, these routes can be overridden easily.
- As long as the API resource (URI route) is respected and supported, extensions can be upgraded easier without causing issues with other extensions (such as incompatible method calls, class name changes etc).
- Classes can still be overridden through Laravel's powerful [Event Listeners](http://laravel.com/docs/events) which can be setup within your extnesion's classes or on an [extension's declaration](/manuals/demo/preparing/declaring) (`extension.php`) level. The choice is yours.

####API Overview

The API in Platform is very easy to use. It any number of [HTTP verbs](http://stackoverflow.com/questions/2001773/understanding-rest-verbs-error-codes-and-authentication#answer-2022938), and has helper methods for 4 of them:

1. GET
2. POST
3. PUT
4. DELETE

Usage is very simple. The first parameter is the URI string and the second parameter is an array of parameters to go to that resource path (such as a query string or POST data, both accessible via Input::get() on the API controller's end).

Below are some examples to put this into context for you:

	// Get data from a resource path
	API::get('some/resource/path');
	
	// Get data from a resource path with Input::get() parameters available
	API::get('some/resource/path', array(
		'foo' => 'bar',
		'baz' => 'bat',
	)):
	
	// Post data to a resource path
	API::post('another/resource/path', array(
		'id'   => 5,
		'name' => 'Ben Corlett',
		'age'  => 20,
	));

>**Notes:** The URI string is prepended with `api/` to determine the actual URI string. `some/resource/path` will actually route to `api/some/resource/path`. Absence of `api/` is purely for convenience.

You can use any number of [HTTP verbs](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods) you want, just use the `API::call()` method:

	// The second parameter is the 
	API::call('some/resource/path', 'HEAD', array(
		'foo' => 'bar',
		'baz' => 'bat',
	));

----------
