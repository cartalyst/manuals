###Users

----------

#### Introduction

The users extension is used to find and edit information about your applications users.  This extension contains two main sections, users and groups, which allow you to search, find, create, edit and delete users and groups.  You will also find user and group permission settings within the create and edit pages of these sections.

----------

#### Screencast

----------

#### Basic Usage

##### Widgets

*Frontend Forms*
- login:    `@widget('platform.users::form.login')`
- register: `@widget('platform.users::form.register')`
- reset:    `@widget('platform.users::form.reset')`

*Backend Forms*
- user create:       `@widget('platform.users::admin.users.form.create')`
- user edit:         `@widget('platform.users::admin.users.form.edit', user_id)`
- user permissions:  `@widget('platform.users::admin.users.form.permissions', user_id)`

- group create:       `@widget('platform.users::admin.groups.form.create')`
- group edit:         `@widget('platform.users::admin.groups.form.edit', user_id)`
- group permissions:  `@widget('platform.users::admin.groups.form.permissions', user_id)`

----------

#### API Functionality


##### Auth

**Login**
Logs a user in

<table>
	<tr>
		<th>Type</th>
		<td>POST</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users/login</td>
	</tr>
	<tr>
		<th>Paramaters</th>
		<td>email, password, remember ( optional )</td>
	</tr>
</table>

*Example*
	
	$response = API::post('users/login', array(
		'email'    => 'john.doe@getplatform.com',
		'password' => 'somepassword',
		'remember' => 1
	));

	if ( ! $response['status'])
	{
		// login failed
	}


**Logout**
Logs a user out

<table>
	<tr>
		<th>Type</th>
		<td>GET</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users/logout</td>
	</tr>
</table>

*Example*
	
	$response = API::get('users/logout');


**Reset Password**
Resets a users password and sends an activation link to activate it.

<table>
	<tr>
		<th>Type</th>
		<td>POST</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users/reset_password</td>
	</tr>
	<tr>
		<th>Paramaters</th>
		<td>email, password</td>
	</tr>
</table>

*Example*
	
	$response = API::post('users/reset_password', array(
		'email'    => 'john.doe@getplatform.com',
		'password' => 'somepassword',
	));

	if ( ! $response['status'])
	{
		// login failed
	}


**Reset Password Confirm**
Confirms a password reset

<table>
	<tr>
		<th>Type</th>
		<td>POST</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users/reset_password_confirm</td>
	</tr>
	<tr>
		<th>Paramaters</th>
		<td>email, password</td>
	</tr>
</table>

*Example*
	
	$response = API::post('users/reset_password_confirm', array(
		'email'    => 'john.doe@getplatform.com',
		'password' => 'somepasswordhash',
	));

	if ( ! $response['status'])
	{
		// login failed
	}


##### Users

**Get Users**
Returns users and related data

<table>
	<tr>
		<th>Type</th>
		<td>GET</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users</td>
	</tr>
	<tr>
		<th>Paramaters</th>
		<td>select, where, order_by, take, skip</td>
	</tr>
</table>

*Example*
	
	$response = API::get('users', array(
		'where' => array(
			array('id', '>', '5')
		),
		'take' => 5,
		'skip' => 0
	));

	if ( ! $response['status'])
	{
		// issue with api request
	}

	$users = $response['users'];


**Register**
Register a user and send an email for activation

<table>
	<tr>
		<th>Type</th>
		<td>POST</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users/register</td>
	</tr>
	<tr>
		<th>Paramaters</th>
		<td>user array.</td>
	</tr>
</table>

*Example*
	
	$response = API::post('users/register', array(
		'email'            => 'john.doe@getplatform.com',
		'password'         => 'somepassword',
		'password_confirm' => 'somepassword',
		'metatdata' => array(
			'first_name' => 'John',
			'last_name'  => 'Doe',
		)
	));

	if ( ! $response['status'])
	{
		// registration failed
	}


**Create**
Create a user

<table>
	<tr>
		<th>Type</th>
		<td>POST</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users/create</td>
	</tr>
	<tr>
		<th>Paramaters</th>
		<td>user array.</td>
	</tr>
</table>

*Example*
	
	$response = API::post('users/create', array(
		'email'            => 'john.doe@getplatform.com',
		'password'         => 'somepassword',
		'password_confirm' => 'somepassword',
		'metatdata' => array(
			'first_name' => 'John',
			'last_name'  => 'Doe',
		)
	));

	if ( ! $response['status'])
	{
		// create failed
	}


**Activate**
Activate a user

<table>
	<tr>
		<th>Type</th>
		<td>POST</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users/activate</td>
	</tr>
	<tr>
		<th>Paramaters</th>
		<td>array with `email` and `code` hashes.</td>
	</tr>
</table>

*Example*
	
	$response = API::post('users/activate', array(
		'email' => $email,
		'code'  => $code,
	));

	if ( ! $response['status'])
	{
		// activation failed
	}


**Update**
Update a user

<table>
	<tr>
		<th>Type</th>
		<td>POST</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users/update</td>
	</tr>
	<tr>
		<th>Paramaters</th>
		<td>user array. `id` required</td>
	</tr>
</table>

*Example*
	
	$response = API::post('users/update', array(
		'id'               => 1,
		'email'            => 'john.doe@getplatform.com',
		'password'         => 'somepassword',
		'password_confirm' => 'somepassword',
		'metatdata' => array(
			'first_name' => 'John',
			'last_name'  => 'Doe',
		)
	));

	if ( ! $response['status'])
	{
		// update failed
	}


**Delete**
Delete a user

<table>
	<tr>
		<th>Type</th>
		<td>POST</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users/delete</td>
	</tr>
	<tr>
		<th>Paramaters</th>
		<td>user array. `id` required</td>
	</tr>
</table>

*Example*
	
	$response = API::post('users/delete', array(
		'id' => 1,
	));

	if ( ! $response['status'])
	{
		// delete failed
	}


**Datatable**
Retrieve Users Datatable data

<table>
	<tr>
		<th>Type</th>
		<td>GET</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users/datatable</td>
	</tr>
	<tr>
		<th>Paramaters</th>
		<td>select, alias, where, order_by</td>
	</tr>
</table>

*Example*
	
	// Grab our datatable
	$response = API::get('users/datatable', Input::get());

	$data = array(
		'columns' => $response['columns'],
		'rows'    => $response['rows'],
	);

	// If this was an ajax request, only return the body of the datatable
	if (Request::ajax())
	{
		return json_encode(array(
			"content"        => Theme::make('users::user.partials.table_users', $data)->render(),
			"count"          => $response['count'],
			"count_filtered" => $response['count_filtered'],
			"paging"         => $response['paging'],
		));
	}

	return Theme::make('users::user.index', $data);

	##### Users

**Get Groups**
Returns groups and related data

<table>
	<tr>
		<th>Type</th>
		<td>GET</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users/groups</td>
	</tr>
	<tr>
		<th>Paramaters</th>
		<td>select, where, order_by, take, skip</td>
	</tr>
</table>

*Example*
	
	$response = API::get('users/groups', array(
		'where' => array(
			array('id', '>', '5')
		),
		'take' => 5,
		'skip' => 0
	));

	if ( ! $response['status'])
	{
		// issue with api request
	}

	$users = $response['users'];


**Create**
Create a group

<table>
	<tr>
		<th>Type</th>
		<td>POST</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users/groups/create</td>
	</tr>
	<tr>
		<th>Paramaters</th>
		<td>user array.</td>
	</tr>
</table>

*Example*
	
	$response = API::post('users/groups/create', array(
		'name' => 'editor',
	));

	if ( ! $response['status'])
	{
		// create failed
	}



**Update**
Update a group

<table>
	<tr>
		<th>Type</th>
		<td>POST</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users/groups/update</td>
	</tr>
	<tr>
		<th>Paramaters</th>
		<td>user array. `id` required</td>
	</tr>
</table>

*Example*
	
	$response = API::post('users/groups/update', array(
		'id'          => 1
		'name'        => 'editor',
		'permissions' => array(),
	));

	if ( ! $response['status'])
	{
		// create failed
	}


**Delete**
Delete a group

<table>
	<tr>
		<th>Type</th>
		<td>POST</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users/groups/delete</td>
	</tr>
	<tr>
		<th>Paramaters</th>
		<td>user array. `id` required</td>
	</tr>
</table>

*Example*
	
	$response = API::post('users/groups/delete', array(
		'id' => 1,
	));

	if ( ! $response['status'])
	{
		// delete failed
	}


**Datatable**
Retrieve Groups Datatable data

<table>
	<tr>
		<th>Type</th>
		<td>GET</td>
	</tr>
	<tr>
		<th>Call</th>
		<td>users/groups/datatable</td>
	</tr>
	<tr>
		<th>Paramaters</th>
		<td>select, alias, where, order_by</td>
	</tr>
</table>

*Example*
	
	// Grab our datatable
	$response = API::get('users/groups/datatable', Input::get());

	$data = array(
		'columns' => $response['columns'],
		'rows'    => $response['rows'],
	);

	// If this was an ajax request, only return the body of the datatable
	if (Request::ajax())
	{
		return json_encode(array(
			"content"        => Theme::make('users::user.partials.table_users', $data)->render(),
			"count"          => $response['count'],
			"count_filtered" => $response['count_filtered'],
			"paging"         => $response['paging'],
		));
	}

	return Theme::make('users::groups.index', $data);