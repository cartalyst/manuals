###Controller

----------

###Aim

For our API to work, we need to create an API controller.

Our API is going to respond to the following resource paths:

	GET  /api/books/datatable
	GET  /api/books
	POST /api/books

#####GET /api/books/datatable

This method returns an array of information used for creating a "Platform Table" - an AJAX driven table used for displaying records in the administration interface.

#####GET /api/books

If the ID of a book is passed through as a parameter, we return that book. If the ID isn't passed through, we return all books.

#####POST /api/books

This method is used to create or update a book. Information is passed through about the book and we create or update a model instance accordingly and return the created model instance.


####Creating controller

lorem ipsum

----------
