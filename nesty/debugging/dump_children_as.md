###dump_children_as($format, $name = null)

This method is an alias for <a href="#dump-as">dump_as()</a>. This method provides 'children' as the third parameter for that method, saving you writing it each time.
<table>
	<tr>
		<th>Parameters</th>
		<td><table class="parameters">
				<tr>
					<th>Param</th>
					<th>Type</th>
					<th>Default</th>
					<th>Description</th>
				</tr>
				<tr>
					<td><kbd>$format</kbd></td>
					<td>string</td>
					<td></td>
					<td>
						The format to dump in. Can be:
						<br>
						<kbd>array</kbd> | <kbd>ul</kbd> | <kbd>ol</kbd> | <kbd>json</kbd> | <kbd>xml</kbd> | <kbd>serialized</kbd> | <kbd>php</kbd>
					</td>
				</tr>
				<tr>
					<td><kbd>$name</kbd></td>
					<td>string</td>
					<td>null</td>
					<td>
						The name of the property to use for each dumped item. Defaults to the <a href="#configure-nesty-cols">name nesty column</a>. A closure can be provided as this parameter. The closure takes one parameter, the Nesty object that's being dumped at that point in time.
					</td>
				</tr>
			</table></td>
	</tr>
	<tr>
		<th>Returns</th>
		<td>mixed</td>
	</tr>
</table>
