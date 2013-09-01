```
title: "Command Line Interface"
```

<table>
	<tr>
		<td>`docpad run`</td>
		<td>Create a website (if one doesn’t exist), watch for changes, and start the webserver</td>
	</tr>

	<tr>
		<td>`docpad scaffold`</td>
		<td>Generate a website from an existing skeleton</td>
	</tr>

	<tr>
		<td>`docpad generate`</td>
		<td>Generate website</td>
	</tr>

	<tr>
		<td>`docpad watch`</td>
		<td>Watch website for changes, and regenerate whenever a change is made</td>
	</tr>

	<tr>
		<td>`docpad server`</td>
		<td>Run the DocPad server (to access an already-generated generated website)</td>
	</tr>

	<tr>
		<td>`docpad render filePath`</td>
		<td>Render standalone files with DocPad programmatically (outputs to STDOUT)</td>
	</tr>

	<tr>
		<td>`docpad render inputMarkdownFile.html.md > outputMarkdownFile.html`</td>
		<td>Render a markdown file, and save the resulting output to a file</td>
	</tr>

	<tr>
		<td>`echo $content | docpad render sampleFileNameWithExtensions`</td>
		<td>Render STDIN with DocPad programmatically (outputs to STDOUT)</td>
	</tr>

	<tr>
		<td>`echo "**awesome**" | docpad render input.html.md > output.html`</td>
		<td>Render passed-in markdown, and save the resulting output to a file</td>
	</tr>

</table>