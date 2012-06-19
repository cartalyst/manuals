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
We need to create a table of contents for our manual. It consists of a title, subtitle and list of links to chapters in the manual.

Create a file at `toc.md` and insert the following:

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

For brevity's sake, we'll just work on the `Steps` chapter only.

Open up `steps/toc.md` and Insert the following:

	##Steps
	####Steps to making a cup of coffee.

	* [Coffee](#markdown "/manuals/coffee/steps/coffee")
	* [Water](#folder_structure "/manuals/coffee/steps/water")
	* [Milk](#create_manual "/manuals/coffee/steps/milk")

Now, we need to create three markdown files to match the `steps/toc.md` file above. They are `coffee.md`, `water.md` and `milk.md`. They're put inside the `coffee/steps/` directory, like so:

	ingredients/
	|   toc.md
	steps/
	|   toc.md
	|   coffee.md
	|   water.md
	|   milk.md

In `steps/coffee.md` insert the following content:

	Put a teaspoon of instant coffee into the mug.
	![Teaspoon of Coffee](http://pad2.whstatic.com/images/thumb/c/c7/Make-a-Cup-of-Instant-Coffee-Step-1.jpg/500px-Make-a-Cup-of-Instant-Coffee-Step-1.jpg)

In `steps/water.md` insert the following content:

	Fill 3/4 of the cup with the boiling hot water, then stir with the teaspoon until all the instant coffee is dissolved.
	![Add Water](http://pad1.whstatic.com/images/thumb/f/f4/Make-a-Cup-of-Instant-Coffee-Step-3.jpg/500px-Make-a-Cup-of-Instant-Coffee-Step-3.jpg)

In `steps/milk.md` insert the following content:

	Fill the remaining 1/4 of the mug with milk. Stir with the teaspoon again.
	![Teaspoon of Coffee](http://pad2.whstatic.com/images/thumb/c/c7/Make-a-Cup-of-Instant-Coffee-Step-1.jpg/500px-Make-a-Cup-of-Instant-Coffee-Step-4.jpg)

Congratulations, you've now on track to making your first manual. You have:

1. Created a manual directory, `/platform/storage/manuals/coffee/`
2. Created a table of contents file that has an introduction and chapter listing
3. Created directories for each chapter
4. Created a table of contents for each chapter that contains links to each article within the chapter. Additionally, you have created three articles for your first chapter.

----------
