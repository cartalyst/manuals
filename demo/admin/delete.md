###Deleting A Book

----------

What good would **CRU** be? Obviously we need the ability to delete a book.

Remember back in the [List All Books](#list) section we setup the `table_books` partial view? Inside that, we had an anchor setup for each book to delete it:

	<a class="btn btn-danger" href="{{ URL::to_secure(ADMIN.'/books/delete/'.$row['id']) }}" onclick="return confirm('{{ Lang::line('platform/books::books.delete.confirm') }}');">{{ Lang::line('button.delete') }}</a>

This shows a button to delete a book, with a JavaScript confirm first. If the user accepts the JavaScript confirm, the person is redirected to the admin screen.

So what's inside that screen? It's pretty straight-forward:

	public function get_delete($id)
	{
		try
		{
			// Make a DELETE API request.
			API::delete('books/'.$id);

			Platform::messages()->success(Lang::line('platform/books::books.delete.success')->get());
		}
		catch (APIClientException $e)
		{
			Platform::messages()->error($e->getMessage());

			foreach ($e->errors() as $error)
			{
				Platform::messages()->error($error);
			}
		}

		// Back to list screen
		return Redirect::to_secure(ADMIN.'/books');
	}

Rather easy right?

Congratulations! You've successfully completed the administration area of your theme!

----------
