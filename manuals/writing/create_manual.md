###Create a Manual - A Guided Tutorial

----------

Let's go through creating a manual. For argument's sake our manual we're writing will be **How to make a cup of coffee**. All directories or files listed in this tutorial assume you have a default installation of Platform and you haven't moved directories around.

----------

####Step 1 - Create manual directory
Create the following directory structure in your Platform's root directory:

	/platform/storage/manuals/coffee/

>**Notes:** All future folder referneces that are relative (no leading slash) are relative to the above directory. `foo/bar.md` is really `/platform/storage/manuals/coffee/foo/bar.md` and so on.

----------

####Step 2 - Create table of contents for manual
We need to create a table of contents for our manual. It consists of a title, subtitle and list of links to chapters in the manual:

	#Making Coffee
	##Lean how to make a cup of coffee.

	* [Ingredients](/manuals/coffee/ingredients)
	* [Steps](/manuals/coffee/steps)

----------

####Step 3 - Create directories for each chapter
Each chapter is a directory within the `coffee/` directory. Each chapter requires a `toc.md` file and relevent article files (explained later).

Because we created two chapters in our table of contents, we need to create the following directory / file structure in our manual:
	
	ingredients/
	|   toc.md
	steps/
	|   toc.md

----------

####Step 4 - Your first article
A chapter (in our example, our chapters are `Ingredients` and `Steps`) consists of a chapter table of contents and articles.

----------
