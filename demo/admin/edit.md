###Creating / Editing a Book

----------

As outlined earlier, our create / edit actions both use the same method. This helps keep our code [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself). When we make a change to the create screen, we don't have to re-do it on the edit screen. We head home earlier and everyone's a winner!

Having said this, let's visit our `get_create()` method in our admin controller:

	public function get_create()
	{
		return $this->get_edit();
	}

Now, let's visit the `get_edit()` method:

	public function get_edit($id = false)
	{
		// Provide a fallback book
		$book = array();

		// If an ID was provided, we're editing
		// a book.
		if ($id)
		{
			try
			{
				$book = API::get('books/'.$id);
			}
			catch (APIClientException $e)
			{
				Platform::messages()->error($e->getMessage());

				foreach ($e->errors() as $error)
				{
					Platform::messages()->error($error);
				}

				// Back to list screen.
				return Redirect::to_secure(ADMIN.'/books');
			}
		}

		return Theme::make('platform/books::edit')
		            ->with('book', $book)
		            ->with('book_id', (isset($book['id']) and $book['id']) ? $book['id'] : false);
	}

We're not going to be going through every aspect of the edit template, as that's covered in other manuals, Laravel's [Templating](http://laravel.com/docs/views/templating) docs, [videos](http://www.screenr.com/ft28) and Laravel's [Form](http://laravel.com/docs/views/forms) docs.

Below is an edit view we could use:

	@layout('templates.default')

	@section('title')
		{{ Lang::line('platform/books::books.'.($book_id ? 'update' : 'create').'.title') }}
	@endsection

	<!-- Scripts -->
	@section('scripts')
		{{ Theme::queue_asset('bootstrap-tab', 'js/bootstrap/tab.js', 'jquery') }}
		{{ Theme::queue_asset('books-edit', 'platform/books::js/edit.js', array('jquery', 'bootstrap-tab')) }}
	@endsection

	@section('content')
	<section id="books-edit">

		<header class="head row">
			<div class="span4">
				<h1>{{ Lang::line('platform/books::books.'.($book_id ? 'update' : 'create').'.title') }}</h1>
				<p>{{ Lang::line('platform/books::books.'.($book_id ? 'update' : 'create').'.description') }}</p>
			</div>
		</header>

		<hr>

		{{ Form::open(null, 'POST', array('enctype' => 'multipart/form-data')) }}
			{{ Form::token() }}

			<ul class="nav nav-tabs">
				<li class="active">
					<a href="#books-general" data-toggle="tab">{{ Lang::line('platform/books::books.tabs.general') }}</a>
				</li>
				<li>
					<a href="#books-cover" data-toggle="tab">{{ Lang::line('platform/books::books.tabs.cover') }}</a>
				</li>
			</ul>

			<div class="tab-content">

				<div class="tab-pane active" id="books-general">
					<div class="well">

						<fieldset>

							{{ Form::label('title', Lang::line('platform/books::books.general.book_title')) }}
							{{ Form::text('title', Input::old('title', array_get($book, 'title')), array('placeholder' => Lang::line('platform/books::books.general.book_title'))) }}

							{{ Form::label('author', Lang::line('platform/books::books.general.author')) }}
							{{ Form::text('author', Input::old('author', array_get($book, 'author')), array('placeholder' => Lang::line('platform/books::books.general.author'))) }}

							{{ Form::label('description', Lang::line('platform/books::books.general.book_description')) }}
							{{ Form::textarea('description', Input::old('description', array_get($book, 'description')), array('placeholder' => Lang::line('platform/books::books.general.book_description'))) }}

							{{ Form::label('link', Lang::line('platform/books::books.general.link')) }}
							{{ Form::url('link', Input::old('link', array_get($book, 'link')), array('placeholder' => Lang::line('platform/books::books.general.link'))) }}

							{{ Form::label('price', Lang::line('platform/books::books.general.price')) }}

							<div class="controls">
								<div class="input-prepend">
									<span class="add-on">$</span>
									{{ Form::number('price', Input::old('price', array_get($book, 'price')), array('placeholder' => Lang::line('platform/books::books.general.price'), 'min' => 0, 'step' => '0.50', 'class' => 'input-small')) }}
								</div>
							</div>

							{{ Form::label('Publisher', Lang::line('platform/books::books.general.publisher')) }}
							{{ Form::text('publisher', Input::old('publisher', array_get($book, 'publisher')), array('placeholder' => Lang::line('platform/books::books.general.publisher'))) }}

							{{ Form::label('Year', Lang::line('platform/books::books.general.year')) }}
							{{ Form::number('year', (Input::old('year', array_get($book, 'year'))) ?: date('Y'), array('placeholder' => Lang::line('platform/books::books.general.year'), 'min' => 1600, 'max' => date('Y'))) }}

						</fieldset>

					</div>
				</div>

				<div class="tab-pane" id="books-cover">
					<div id="upload-cover" class="{{ array_get($book, 'cover') ? 'hide' : null }}">
						{{ Form::label('cover', Lang::line('platform/books::books.general.cover')) }}
						{{ Form::file('cover') }}
					</div>
					<div>
						{{ Form::hidden('cover', array_get($book, 'cover'), array('id' => 'existing-cover', 'data-cover' => array_get($book, 'cover'))) }}

						@if (isset($book['cover_url']))
							<div class="row-fluid" id="cover-preview">
								<ul class="thumbnails">
									<li class="span6">
										<div class="thumbnail">
											<img src="{{ $book['cover_url'] }}" alt="{{ $book['cover'] }}">
											<div class="caption">
												<h5>{{ $book['cover'] }}</h5>
												<a href="#" class="btn btn-danger" id="remove-existing-cover">
													{{ Lang::line('platform/books::books.delete.cover') }}
												</a>
											</div>
										</div>
									</li>
								</ul>
							</div>

							<a href="#" class="btn hide" id="undo-remove-existing-cover">
								{{ Lang::line('platform/books::books.delete.undo_cover') }}
							</a>
						@endif
					</div>
				</div>
			</div>

			<div class="form-actions">
				{{ Form::button(Lang::line('platform/books::books.button.'.(($book_id) ? 'update' : 'create')), array('class' => 'btn btn-primary')) }}
				{{ HTML::link(ADMIN.'/books', 'Cancel', array('class' => 'btn')) }}
			</div>

		{{ Form::close() }}
		
	</section>
	@endsection

Now, we need to create another JavaScript file. This time it'll go under `public/platform/themes/backend/default/extensions/books/assets/js/edit.js`. We made a reference to this in the template above.

Insert the following in `edit.js` (The comments in the JavaScript are fairly selft-explanatory):

	// Execute when the DOM is laoded
	$(document).ready(function() {

		// When the user clicks "Remove existing cover", we need
		// to do some stuff
		$('#remove-existing-cover').on('click', function(e) {
			e.preventDefault();

			// Firstly, let's hide the cover's preview
			$('#cover-preview').addClass('hide');

			// We empty the cover input value. This will
			// Remove it from the model when it's aved
			$('#existing-cover').val('');

			// Show the upload button so that the user
			// can upload a new cover
			$('#upload-cover').removeClass('hide');

			// Show an undo button so they can undo their changes.
			$('#undo-remove-existing-cover').removeClass('hide');
		});

		// When user clicks on the undo button
		$('#undo-remove-existing-cover').on('click', function(e) {

			// Let's hide the undo button
			$(this).addClass('hide');

			// We hide the upload button as we're
			// showing the old cover's preview
			$('#upload-cover').addClass('hide');

			// Reinstate the existing cover input
			// value. We stored the original value
			// in [data-cover=""] within the <input>
			// tag on the DOM
			var $input = $('#existing-cover');
			$input.val($input.data('cover'));

			// Show the cover preview again. Once
			// we've done this, we've reversed the
			// hiding process, thus achieving an
			// 'undo'.
			$('#cover-preview').removeClass('hide');
		});

	});

In a nutshell, the JavaScript handles managing book covers nice. It allows you do remove existing covers and add new ones. You can even undo your changes should you change your mind, without reloading the entire page.

####POSTing Our Data

Now, we need to create the actions corresponding to posting our form.

The first action, `post_create()` is much like `get_create()`:

	public function post_create()
	{
		return $this->post_edit();
	}

The section action, `post_edit()` is where the magic happens:

	public function post_edit($id = false)
	{
		// Get input data.
		$data = Input::get();

		try
		{
			// If there is an ID, do a PUT request to
			// the API
			if ($id)
			{
				API::put('books/'.$id, $data);

				Platform::messages()->success(Lang::line('platform/books::books.update.success')->get());
			}

			// If there isn't an ID, we're
			// creating a new book
			else
			{
				API::post('books', $data);

				Platform::messages()->success(Lang::line('platform/books::books.create.success')->get());
			}
		}
		catch (APIClientException $e)
		{
			Platform::messages()->error($e->getMessage());

			foreach ($e->errors() as $error)
			{
				Platform::messages()->error($error);
			}

			// Back to edit screen. Also
			// include the input they previously
			// had so they don't lose their changes.
			return Redirect::to_secure(ADMIN.'/books/'.(($id) ? 'edit/'.$id : 'create'))->with_input();
		}

		// On successful requests, we just
		// redirect back to the list screen.
		return Redirect::to_secure(ADMIN.'/books');
	}

----------
