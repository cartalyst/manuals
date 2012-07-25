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
