```
title: "Quick Start"
```
## Quick Start from a Pre-Made Website

If you want to use one of our [pre-made websites](/docpad/skeletons) to get up and running real quickly, just run the following:

``` bash
mkdir my-website
cd my-website
docpad run
```

This will ask you which pre-made website you'd like to use (or even if you don't want to use one). Once you've picked one, we'll clone it into the current working directory, generate it, watch for changes, and fire up our inbuilt webserver at [http://localhost:9778/](http://localhost:9778/) so you can see your website right away! How awesome!


## Quick Start from Scratch

If you'd rather get your hands dirty by making your own basic website from scratch, here's the steps:

1. Create a directory for your website, get inside of it and initialize an empty docpad project:

	``` bash
	mkdir my-website
	cd my-website
    docpad init
	```

1. Install the [Eco](http://docpad.org/plugin/eco) and [Marked](http://docpad.org/plugin/marked) rendering plugins:

	``` bash
	docpad install eco,marked
	```

1. Create the following files:

	1. A layout at `src/layouts/default.html.eco` that contains:

		``` erb
		<html>
		<head>
			<title><%= @document.title %></title>
			<%- @getBlock("meta").toHTML() %>
			<%- @getBlock("styles").toHTML() %>
		</head>
		<body>
			<%- @content %>
			<%- @getBlock("scripts").toHTML() %>
		</body>
		</html>
		```

	2. Another layout at `src/layouts/post.html.eco` that contains:

		``` erb
		---
		layout: default
		---
		<h1><%= @document.title %></h1>
		<div><%- @content %></div>
		```

	3. A document at `src/documents/posts/hello.html.md` that contains:

		``` html
		---
		layout: post
		title: Hello World!
		---
		Hello **World!**
		```

1. Then, when you generate your website by running `docpad run`
	
	1. You will get an html file at `out/posts/hello.html` that contains:

		``` html
		<html>
		<head>
			<title>Hello World!</title>
		</head>
		<body>
			<h1>Hello World!</h1>
			<div>Hello <strong>World!</strong></div>
		</body>
		</html>
		```
		
	1. And any files inside the `src/files` directory will be copied to the `out` directory, e.g. `src/files/styles/style.css` -> `out/styles/style.css`

1. Awesome. Now, how were the `<%=...%>` and `<%-...%>` parts substituted?

	1. This is possible because we parse the documents and layouts through a template rendering engine. In this example, we use a template rendering engine called [Eco](https://github.com/sstephenson/eco) (hence the `.eco` extensions of the layouts). Templating engines allows you to do some pretty nifty things! In fact, we could display all the titles and links of our posts with the following:

		``` erb
		<% for post in @getFilesAtPath("posts").toJSON(): %>
			<a href="<%= post.url %>"><%= post.title %></a><br/>
		<% end %>
		```

	3. The `@getBlock` stuff is used so plugins can easily add new meta, scripts and styles to our website. For instance, the [livereload plugin](/plugin/livereload) that reloads our webpage whenever a regeneration occurs will inject a script into our script block, which is then output to our page when we do the `<%- @getBlock("scripts").toHTML() %>` in our layout :)

1. Cool. Now how did `Hello **World!**` in our document get converted into `Hello <strong>World!</strong>`?

	1. That was possible as the file was a [Markdown](http://daringfireball.net/projects/markdown/basics) file (hence its `.md` extension). Markdown is fantastic for working with text-based documents, as it really allows you to focus on your content instead of the syntax for formatting the document!

1. Fantastic! Thanks for that! Continue on with the guide to learn a lot more. This was just the tip of the iceberg, and there's plenty of opt-in awesomeness yet to be discovered.
