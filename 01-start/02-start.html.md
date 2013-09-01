```
title: "Quick Start"
```


## Quick Start from a Pre-Made Website

If you want to use one of our [pre-made websites](/docpad/skeletons) to get up and running quickly, just run the following:

``` bash
mkdir my-website
cd my-website
docpad run
```

This will ask you which pre-made website to use (even if you don’t want to use one). Once you’ve chosen, DocPad will clone it into the current working directory, `generate` it, `watch` for changes, and fire up the built-in web server at [http://localhost:9778/](http://localhost:9778/). You’ll be able to see your site right away! Awesome. :)


## Quick Start from Scratch

If you’d rather make your own website from scratch, here’show:

1. Create a directory for your website, and change to it

1. Initialize an empty DocPad project:

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

	1. The layout file `src/layouts/default.html.eco`, with the contents:

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

	2. The layout file `src/layouts/post.html.eco`, with the contents:

		``` erb
		---
		layout: default
		---
		<h1><%= @document.title %></h1>
		<div><%- @content %></div>
		```

	3. The document `src/documents/posts/hello.html.md`, with the contents:

		``` html
		---
		layout: post
		title: Hello World!
		---
		Hello **World!**
		```

1. Generate your website with `docpad run`
	
	1. You’ll get a HTML file at `out/posts/hello.html`, with the contents:

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
		
	1. Any files in `src/files/` directory will be copied to `out/` directory. E.g. `src/files/styles/style.css` → `out/styles/style.css`

1. Awesome. Now, how did the `<%=...%>` and `<%-...%>` parts get substituted away?

	1. This is possible because DocPad parses the documents and layouts with **template rendering engine**. In this example, we used the template rendering engine [Eco](https://github.com/sstephenson/eco) (hence the `.eco` extensions of the layouts). Templating engines allows you to do some pretty nifty things. In fact, we could display all the titles and links of our posts with the following:

		``` erb
		<% for post in @getFilesAtPath("posts").toJSON(): %>
			<a href="<%= post.url %>"><%= post.title %></a><br/>
		<% end %>
		```

	3. The `@getBlock()` stuff is allows plugins to easily add new meta, scripts, and styles to your site. For instance, the [livereload plugin](/plugin/livereload) reload your whenever a regeneration occurs. It injects a script into your script block, which is output to your page with `<%- @getBlock("scripts").toHTML() %>` in the layout.

1. Cool. Now how did `Hello **World!**` in the document get converted into `Hello <strong>World!</strong>`?

	1. That file was a [Markdown](http://daringfireball.net/projects/markdown/basics) file (hence the `.md` extension it had). Markdown is fantastic for working with text-based documents, as it really allows you to focus on the content.

1. Fantastic! Thanks for that! Continue the guide to learn lots more. This was just the tip of the iceberg; there’s a lot more awesomeness you can opt-in to.

