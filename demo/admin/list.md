###Listing All Books

----------

Platform comes with it's own great jQuery plugin that allows you to manage items within a table very easily. Remember how we created an API method to return the data required for a datatable? We're going to use that now.

	public function get_index()
	{
		try
		{
			// Grab our datatable
			$datatable = API::get('books/datatable', Input::get());
		}
		catch (APIClientException $e)
		{
			Platform::messages()->error($e->getMessage());

			foreach ($e->errors() as $error)
			{
				Platform::messages()->error($error);
			}

			// We have nowhere else to go, let's
			// just go back to the dashboard.
			return Redirect::to_secure(ADMIN);
		}

		$data = array(
			'columns' => $datatable['columns'],
			'rows'    => $datatable['rows'],
		);

		// If this was an ajax request, only return the body of the datatable
		if (Request::ajax())
		{
			return json_encode(array(
				'content'        => Theme::make('books::partials.table_books', $data)->render(),
				'count'          => $datatable['count'],
				'count_filtered' => $datatable['count_filtered'],
				'paging'         => $datatable['paging'],
			));
		}

		// Return the books list view
		return Theme::make('books::index', $data);
	}

In the admin controller method above, you'll have noticed that we have returned two Theme views. Let's go ahead and create the following two files:

- `public/platform/themes/backend/default/extensions/books/index.blade.php`
- `public/platform/themes/backend/default/extensions/books/partials/table_books.blade.php`


####Platform Admin Templates

Platform uses Laravel's wonderful [Blade templating engine](http://laravel.com/docs/views/templating) to render it's Theme templates.

The layout for our admin theme (`public/platform/themes/backend/default/extensions/books/index.blade.php`) is as such:

	<!-- This can be another template if you choose -->
	@layout('templates.default')
	
	@section('title')
		<!-- This is the page title -->
	@endsection
	
	@section('styles')
		<!-- This is where you can queue theme styles with their dependencies -->
	@endsection
	
	<!-- This is where you can queue theme scripts with their dependencies -->
	
	@section('scripts')
		<!-- This is where you include any inline javascripts -->
	@endsection
	
	@section('content')
		<!-- The main page content section -->	
	@endsection

Knowing this, let's go and create our list template

	@layout('templates.default')

	@section('title')
		{{ Lang::line('books::books.general.title') }}
	@endsection

	@section('links')
		{{ Theme::asset('css/table.css') }}
	@endsection

	<!-- Scripts -->
	@section('scripts')
		{{ Theme::queue_asset('table', 'js/table.js', 'jquery') }}
		{{ Theme::queue_asset('books-index', 'books::js/index.js', array('jquery', 'table')) }}
	@endsection


	@section('content')

		<!-- Include the title and description for the page -->
		<header class="head row">
			<div class="span6">
				<h1>{{ Lang::line('books::books.general.title') }}</h1>
				<p>{{ Lang::line('books::books.general.description') }}</p>
			</div>
		</header>

		<!-- And a horizontal divider -->
		<hr>

		<!-- This is the container for our table -->
		<div id="table">

			<!-- Table actions are where we put our buttons such as "Create" -->
			<div class="actions clearfix">
				<div id="table-filters" class="form-inline pull-left"></div>
				<div class="pull-right">
					<a class="btn btn-large btn-primary" href="{{ URL::to_secure(ADMIN.'/books/create') }}">{{ Lang::line('books::books.button.create') }}</a>
				</div>
			</div>

			<!-- This is the standard markup required for a Platform table -->
			<div class="row">
				<div class="span12">
					<div class="row">
						<ul id="table-filters-applied" class="nav nav-tabs span10"></ul>
					</div>
					<div class="row">
						<div class="span10">
							<div class="table-wrapper">
								<table id="books-table" class="table table-bordered">
									<thead>
										<tr>
											@foreach ($columns as $key => $col)
											<th data-table-key="{{ $key }}">{{ $col }}</th>
											@endforeach
											<th></th>
										</tr>
									<thead>
									<tbody>

									</tbody>
								</table>
							</div>
						</div>
						<div class="tabs-right span2">
							<div class="processing"></div>
							<ul id="table-pagination" class="nav nav-tabs"></ul>
						</div>
					</div>
				</div>
			</div>

		</div>

	@endsection

Now, we have the template ready, but there's no content inside the table. We need to do two more things:

1. Create a partial view that represents what's returned from the platform table.
2. Create some javascript to enable the jQuery plugin that manages the table for us.

####Partial View

Open up `public/platform/themes/backend/default/extensions/books/partials/table_books.blade.php` and insert the following:

	@foreach ($rows as $row)
		<tr>
			<td class="span1">{{ $row['id'] }}</td>
			<td class="span2">{{ $row['title'] }}</td>
			<td class="span1">{{ $row['author'] }}</td>
			<td class="span1">${{ number_format($row['price'], 2) }}</td>
			<td class="span1">{{ $row['year'] }}</td>
			<td class="span2">
				<a class="btn" href="{{ URL::to_secure(ADMIN.'/books/edit/'.$row['id']) }}">{{ Lang::line('button.edit') }}</a>
				<a class="btn btn-danger" href="{{ URL::to_secure(ADMIN.'/books/delete/'.$row['id']) }}" onclick="return confirm('{{ Lang::line('books::books.delete.confirm') }}');">{{ Lang::line('button.delete') }}</a>
			</td>
		</tr>
	@endforeach

If you look carefully, you'll notice that we're iterating through an array of table rows. Each row is populated with the `select` property of the `$defaults` array defined in our [API Controller's](http://local.getplatform.com/manuals/demo/api#controller) `get_datatable()` method.

Now, we've done all that markup, we need to include a JavaScript library to handle the Platform table.

To do this, we need to make a file called `index.js` and put it under `public/platform/themes/backend/default/extensions/books/assets/js/index.js`.

>**Notes:** Why's it called `index.js`? Because that's what it was called in our template - `{{ Theme::queue_asset('books-index', 'books::js/index.js', array('jquery', 'table')) }}` The first method of `Theme::queue_asset()` is a name to give the asset. The second is the path to the file, where the format is `bundle::path/to/file.js`. The third parameter is an array of dependencies, where each item is the `name` of another asset.

The contents of `index.js` should be:

	// Run the following function when jQuery has
	// successfully loaded.
	(function($) {

		// Call the platform.table plugin. The first
		// parameter is a jQuery selector for the DOM
		// element. The second parameter is an array of
		// options. The only require option is 'url', which
		// is the URL of the contents of the table.
		platform.table.init($('#books-table'), {
			'url': platform.url.admin('books'),
		});
	})(jQuery);

Now, you've got a way of listing all books. But what good would it be if you couldn't create, edit or delete them. Moving on...

----------
