###Introduction

----------

####What Are Extensions?
Extensions are what drive your application.  All of your application logic should be within one or multiple extensions. This is done to make your application completely modular.

Extensions are really just Laravel bundles. We seperated extensions from the bundles directory because we believe helper type bundles should be separated from bundles that are routable or application specific. They also have a few additional requirements, that we'll mention next. These requirements are very small and make the modular approach much cleaner and simpler to work with.

In Platform, we give the ability for multiple extensions to share the same name through vendor separation. This allows for powerful overriding of core functionality.

#####Example Extensions
- Users
- Logs
- Settings

#####Example Bundles
- Sentry ( authentication bundle )
- OAuth
- Swiftmailer

----------
