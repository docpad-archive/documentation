```
title: "Command Line Interface"
```

- To create your website (if it doesn't already exist), watch for changes, and start the webserver, use:

	``` bash
	docpad run
	```

- To just generate your website from one of the existing skeletons, use:

	``` bash
	docpad scaffold
	```

- To just generate your compiled website, use:

	``` bash
	docpad generate
	```

- To just watch your website for changes and re-generate whenever a change is made, use:

	``` bash
	docpad watch
	```

- To just run the DocPad server to access your already generated website, use:

	``` bash
	docpad server
	```

- To render standalone files with DocPad programatically (will output to stdout)

	``` bash
	docpad render filePath
	```

	E.g. To render a markdown file and save the result to an output file, we would use:

	``` bash
	docpad render inputMarkdownFile.html.md > outputMarkdownFile.html
	```

- To render stdin with DocPad programatically (will output to stdout)

	``` bash
	echo $content | docpad render sampleFileNameWithExtensions
	```

	E.g. To render passed markdown content and save the result to a file, we would use:

	``` bash
	echo "**awesome**" | docpad render input.html.md > output.html
	```

