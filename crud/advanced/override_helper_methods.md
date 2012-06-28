###Override Helper Methods

----------

Before and After every primary action (find, insert, update, delete, validation) there is an associated helper function you can override to maniuplate any data or response you wish to fit your application. Example: 'protected function before_insert()'. There is also a `prep_attributes()` method if you wish change attribute values after validation runs, before you insert them into the database.

Below is a full list of override helper methods in Crud:

 - `before_insert($query, columns)`
 - `after_insert($result)`
 - `before_find($query, $columns)`
 - `after_find($result)`
 - `before_all($query, $columns)`
 - `after_all($results)`
 - `before_update($query, $columns)`
 - `after_update($result)`
 - `before_delete($query)`
 - `after_delete($query)`
 - `before_validation($data, $results)`
 - `after_validation($result)`

----------
