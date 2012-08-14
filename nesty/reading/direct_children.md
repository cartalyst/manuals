###direct_children()

----------

The `direct_children` method returns an `array` of children Nesty objects for the Nesty object on which this method was called, where the limit for fetching and hydrating children is 1 level deep. This is purely an alias for `children`.

> <strong>**Notes:**</strong> This method should only be called when you know that you will never need to go more than 1 level deep on recursion. See <a href="#get-children">here</a> for more information.                        |

Parameters                   | Type            | Default       | Description      
:--------------------------- | :-------------: | :------------ | :---------------  
`$columns`                   | array           | array('*')    | Array of columns to select for children. Defaults to all columns.

----------