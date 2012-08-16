###Laravel routes.php

----------

Laravel is amazing and includes a wonderful [Routing](http://laravel.com/docs/routing) system. You can utilize the full functionality of Laravel routes in your extension should you choose. At the bare minimum, you need include a simple routes file. It should be placed under `books/routes.php`:

	<?php

	Route::controller(Controller::detect('books'));

That's it. Really.

----------
