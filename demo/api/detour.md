###A Little Detour

----------

####Information About the Platform API and Why It's Awesome!

Convention states that all methods in an API controller should return a Response. The status of the API request is described with appropriate HTTP status codes, each defined in a constant within the `Platform\API` class:

- **`API::STATUS_OK`** (HTTP status 200 *"Everything is fine, I'm returning what you asked for."*). This status is the default status for a `Response` and is not usually required.
- **`API::STATUS_CREATED`** (HTTP status 204 *"I've created the resource you submitted, but I don't have anything to return."*). This status is returned when a new entity has been created
- **`API::STATUS_NO_CONTENT`** (HTTP status 204). This status is returned when an entity has been deleted. Nothing is to be returned as an entity is deleted, however `API::STATUS_OK` cannot be returned without content.
- **`API::STATUS_MOVED_PERMANENTLY`** (HTTP status 301 *"Anything maintaining links to this resource should update the links to the new location."*). This should be used when your API methods have moved to a new location permanently.
- **`API::STATUS_FOUND`** (HTTP status 302 *"Temporarily available at the new location."*). The resource is only temporarily available at the new location.
- **`API::STATUS_BAD_REQUEST`** (HTTP status 400 *"General error condition, such as malformed input data."*). This status should be returned on all errors that cannot fall into any other `4xx` API statuses.
- **`API::STATUS_UNAUTHORIZED`** (HTTP status 401 *"You need to identify yourself before the request will be able to continue"*). This is when you are trying to access a protected resource but are not authorized. **Note**, normally you should throw a `STATUS_NOT_FOUND` status if unauthorized users cannot know this particular resource exists.
- **`API::STATUS_FORBIDDEN`** (HTTP status 403 *"You have been identified but do not have permission to access this resource or run the requested action."*). This is usually only used as an [ACL](http://en.wikipedia.org/wiki/Access_control_lists) issue response.
- **`API::STATUS_NOT_FOUND`** (HTTP status 404 *"The requested resource does not exist"*). The same 404 that we've all come to know and despise.
- **`API::STATUS_NOT_ALLOWED`** (HTTP status 405 *"The requested HTTP verb is not allowed for this resource"*). This is given when you are using the wrong HTTP verb (`GET`, `POST` etc) to access a resource. This isn't currently used in Platform, but it's here for you to use should you want!
- **`API::STATUS_UNPROCESSABLE_ENTITY`** (HTTP status 422 *"You have provided the right type of data (thus avoiding a 400) but validation failed."*). As description says, model [validation](/manuals/crud/advanced#validation) failed.
- **`API::STATUS_INTERNAL_SERVER_ERROR`** (HTTP status 500 *"General or Unkown error."*). This error should indicate a server error, or what you want API users to see as a server error. Any uncaught Exceptions in the API get caught and returned as this status.
- **`API::STATUS_SERVICE_UNAVAILABLE`** (HTTP status 503 *"Usually indicates app server or database is unavailable."*). Indicates there is an issue within the application connecting to one or more servers or resources.

####Unsuccessful API Requests

Statuses that are considered "unsuccessful" are those that aren't `2xx` or `3xx`. Internally, these statuses are converted to an appropriate `Exception`. This allows you to interact with the API and catch one or more Exceptions based on what happened in the reqeust.

Every "unsuccessful" status has a corresponding Exception class that can be caught.

All "unsuccessful" requests MUST a `Response` where the first parameter is an array and the second parameter is an API Status:

	return new Response(array(
		'message' => "Message about why the request wasn't successful",
		
		// This parameter is OPTIONAL, however
		// if it's included it's contents MUST
		// be an array.
		'errors' => array(
			'Field a was missing',
			"You didn't provide an email address",
		),
	),
	
	// Plus an API status - this
	// particular one is when
	// validation failed
	API::STATUS_UNPROCESSABLE_ENTITY
	);

For all `4xx` statuses, you can catch `APIClientException` as a general Exception, in conjunction with:

- `APIBadRequestException`
- `APIUnauthorizedException`
- `APIForbiddenException`
- `APINotFoundException`
- `APINotAllowedException`
- `APIUnprocessableEntityException`

For all `5xx` statuses, you can catch `APIServerException` as a general Exception, in conjunction with:

- `APIInternalServerErrorException`
- `APIServiceUnavailableException`

All of the API Exceptions extend a class called `APIException`. This class always has an available message which describes the error, retrievable at `APIException::getMessage()`. It also has a method `APIException::errors()`, which returns an array of errors associated with the Exception. For example, an `APIUnprocessableEntityException` (validation failed) Exception's errors() method will return an array of validation error messages. The person can then display these messages however they'd like to.


####Implementing an API Response

The following scenario is and example where we're trying to update a `Car` entity.

	// Find the car
	$car = Car::find($id);
	
	// Method returned null? Car doesn't exist
	if ($car === null)
	{	
		return new Response(array(
			'message' => "Car [$id] coud not be found.",
		), API::STATUS_NOT_FOUND);
	}
	
	// Update the car's attributes
	$car->fill(Input::get());
	
	// See if the car saves
	if ($car->save())
	{
		// Return the updated car.
		// API::STATUS_OK is not required
		// as it's the default second
		// parameter of Response::__construct()
		return new Response($car);
	}
	else
	{
		// Flag whether there were validation errors
		$has_errors = $car->validation()->errors->has();
		
		// If there were errors, we'll return that
		// response
		if ($has_errors)
		{
			return new Response(array(
				'message' => 'Validation failed while updating the car.',
				
				// Note the 'errors' param
				'errors' => $car->validation()->errors->all(),
			), API::STATUS_UNPROCESSABLE_ENTITY);
		}
		
		// If there weren't Validation errors and
		// the car didn't save, return a general
		// error status
		else
		{
			return new Response(array(
				'message' => 'An error occured while updating the car.',
			), API::STATUS_BAD_REQUEST);
		}
	}


----------
