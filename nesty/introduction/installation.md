###Installation

----------

Once downloaded, you may want to add nesty to the always load packages array in 'app/config.php'.

If you don't do this, you will need to call Package::load('nesty'); to register the package with FuelPHP. This is the most efficient way to use any package, as you are only loading the package on requests when you are using it. This only needs to be called once per request.

----------
