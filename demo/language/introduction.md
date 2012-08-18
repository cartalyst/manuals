###Introduction

----------

Platform, at it's heart, is a multilingual system. This means it's theoretically accessible to people of any tongue, as long as there is an appropriate language file.

Currently, Platform is shipping with English (`en`) language files. However, this will increase in the future. This is where you should [fork](https://github.com/cartalyst/platform) and help us.

Laravel has [great documentation](http://laravel.com/docs/localization) on Localizations and Language files. Rather than re-iterate their words, you should have a read up on it if you're not familiar.

By now you've probably realised that we've not been outputting raw strings to the user. If you've been reloading your page as you've been going, you'll have noticed a lot of string that look similar to `books::books.general.ttile`. Let's fix this!

Create a file under `books/language/en/books.php`. Place the following inside it:

	<?php

	return array(

		/* General */
		'general' => array(
			'title'            => 'Books Management',
			'author'           => 'Author',
			'book_title'       => 'Title',
			'book_description' => 'Description',
			'description'      => 'Manage books.',
			'id'               => 'Id',
			'id_required'      => 'A book Id is required.',
			'cover'            => 'Cover',
			'link'             => 'Link',
			'not_found'        => 'Book not found.',
			'price'            => 'Price',
			'publisher'        => 'Publisher',
			'status'           => 'Status',
			'year'             => 'Year',
		),

		/* Buttons */
		'button' => array(
			'create'         => 'Create Book',
			'cancel'         => 'Cancel',
			'delete'         => 'Delete',
			'edit'           => 'Edit',
			'reset_password' => 'Reset',
			'update'         => 'Save Changes',
		),

		/* Create Book */
		'create' => array(
			'title'          => 'Create Book',
			'description'    => 'Please supply the following information.',
			'error'          => 'Book was not created, please try again.',
			'success'        => 'Book created successfully.',
		),

		/* Update Book */
		'update' => array(
			'title'          => 'Update Book',
			'description'    => 'Please update the following information.',
			'error'          => 'Book was not updated, please try again',
			'success'        => 'Book updated successfully.',
		),

		/* Delete Book */
		'delete' => array(
			'cover'      => 'Remove Cover',
			'undo_cover' => 'Undo Cover Removal',
			'confirm'    => 'Are you sure you want to delete this book?',
			'error'      => 'There was an issue deleting the book. Please try again.',
			'success'    => 'The book was deleted successfully.',
		),

		/* Tabs */
		'tabs' => array(
			'general' => 'General',
			'cover'   => 'Cover',
		),

		/* General Errors */
		'errors' => array(
			'not_found'       => 'Book Id: :id doesn\'t exist.',
			'count_error'     => 'There was an issue retrieving the count, please try again.',
			'invalid_request' => 'Not a valid book.',
		)

	);

Now reload your page, you should see a much nicer extension!

----------
