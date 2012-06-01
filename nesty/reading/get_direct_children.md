###get_direct_children()

----------

The <kbd>get_direct_children</kbd> method returns an array of children Nesty objects for the Nesty object on which this method was called, where the limit for fetching and hydrating children is 1 level deep. This is purely an alias for <kbd>get_children</kbd>.

> <strong>Notes:</strong> This method should only be called when you know that you will never need to go more than 1 level deep on recursion. See <a href="#get-children">here</a> for more information.

<table>
	<tr>
		<th>Returns</th>
		<td>array()</td>
	</tr>
</table>