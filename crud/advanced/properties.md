###Crud Properties

----------

Alongside the properties outlined in [Usage](/manuals/crud/usage), there are some other properties that you can specify for Crud. The full list of properties for Crud are shown below

Property                        | Type              | Default       | Description      
:------------------------------ | :-------------:   | :------------ | :---------------  
`protected static $_key`        | int \| string     | id            | The primary key of the table
`protected static $_table`      | string            | null          | The name of the table used by Crud.
`protected static $_connection` | string            | null          | The name of the database connection associated with the model.
`protected static $_sequence`   | string            | null          | The name of the sequence associated with the model.
`protected static $_timestamps` | bool              | false         | Indicates if the model has update and creation timestamps (`created_at` and `updated_at`). These columns must exist.
`protected static $_events`     | bool              | true          | Indicates if the model should use events (on creation, update etc)
`protected static $_rules`      | array             |               | An array of key / value pairs of rules. See Laravel's Validation [docs](http://laravel.com/docs/validation).

----------
