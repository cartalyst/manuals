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
	<tr>
		<th>Returns</th>
		<td>array<br>
			- status: `bool`
			- message: `string` // when false
			- users: `array` // when true
		</td>
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
		<td>user array. <a href="#">See sentry docs</a></td>
	</tr>
</table>

*Example*
	
	$response = API::get('users/register', array(
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
		// issue with api request
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
		<td>user array. <a href="#">See sentry docs</a></td>
	</tr>
</table>

*Example*
	
	$response = API::get('users/register', array(
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
		// issue with api request
	}

	$users = $response['users'];