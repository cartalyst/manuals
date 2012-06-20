###Folder Structure

----------

The default theme for Platform Manuals expects markdown files to be provided in a particular structure.

The directory for Platform Manuals' markdown files is located under `manuals/` in your Platform installation's `storage` folder.

Because Platform Manuals supports multiple manuals, you need to create a sub-directory for each manual. For example:

	Storage
	|   Manuals
	|   |   foo
	|   |   bar
	|   |   baz

>**Notes:** There are currently two reserved names, `edit` and `oauth` as these routes are used in the manuals extension. If you create a manual with this name, it will be ignored.

----------
