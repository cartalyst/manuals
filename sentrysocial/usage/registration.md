###Registration

----------

Once authenticated, registration may or may not be required depending on the provider and what information you want for your application.  Sentry requires an email address, so an email will always be required.

There are 4 possible registration scenarios.

#### User is already logged in via Sentry

If the user is already logged in with Sentry, no further registration will be required.  It will automatically tie the social account with the current logged in user.

#### User is not logged in, but has an account

If the user is not logged in, but does have a Sentry account already, they can log into their sentry account to tie the social account to theirs.

#### User is not logged in and does not have an account

If the user is not logged in, and doesn't have an account their authentication information will be held in a session.  You can then create your own registration page for the required information you may want such as email address and more.  You can then call `SentrySocial::create()` to continue the registration process.

#### User is not logged in but the provider gave us an email

If the user is not logged in but the provider gives us an email, we can auto create an account for them with no further input.  It will be like a registration process did not occur.  If you still wish to have more fields, you can ask for the extra input afterwards.