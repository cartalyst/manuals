###Introduction

----------

Platform at it's core is an API-driven platform^PunIntended. Everything in Platform interacts through an internal [REST-like](http://en.wikipedia.org/wiki/Representational_state_transfer) API. This allows extensions to be de-coupled as they do not need to interact directly with each other's models and classes, but rather the API can return data in standard formats (arrays / JSON). The data is sent from API controllers which respond to a particular URI route which is all controlled by the developer.

De-coupling is a fancy word that essentially means that extensions operate on their own and aren't dramatically affected by the existence / non-existence of other extensions. This is the only way to be truly modular.

In Platform, our extensions are de-coupled because:

- There are no references to direct classes. No more `class doesn't exist` errors if an extension is disabled or overridden.
- Because the API responds to URI routes, these routes can be overridden easily.
- As long as the API resource (URI route) is respected and supported, extensions can be upgraded easier without causing issues with other extensions (such as incompatible method calls, class name changes etc).
- Classes can still be overridden through Laravel's powerful [Event Listeners](http://laravel.com/docs/events) which can be setup within your extnesion's classes or on an [extension's declaration](/manuals/demo/preparing/declaring) (`extension.php`) level. The choice is yours.

----------
