```
title: "Quick Start"
```


## Quick Start from a Pre-Made Website

If you want to use one of our [pre-made websites](/docpad/skeletons) websites to get up and running real quickly, just run the following:

``` bash
mkdir my-website
cd my-website
docpad run
```

This will ask you which pre-made website you'd like to use (or even if you don't want to use one). Once you've picked one, we'll clone it out into the current working directory, generate it, watch for changes, and fire up our inbuilt webserver for the website at [http://localhost:9778/](http://localhost:9778/) so you can see your website right away! How awesome!


## Quick Start from Scratch

If you'd rather get your hands dirty by making your own real basic website from scratch, here's the steps:

1. Create a directory for your website and get into it:

	``` bash
	mkdir my-website
	cd my-website
	```

1. Install the [Eco](http://docpad.org/plugin/eco) and [Marked](http://docpad.org/plugin/marked) rendering plugins:

	``` bash
	npm install --save docpad-plugin-eco docpad-plugin-marked
	```

1. Create the following files:

	1. A layout at `src/layouts/default.html.eco` that contains:

		``` erb
		<html>
		<head><title><%=@document.title%></title></head>
		<body>
			<%-@content%>
		</body>
		</html>
		```

	2. Another layout at `src/layouts/post.html.eco` that contains:

		``` erb
		---
		layout: default
		---
		<h1><%=@document.title%></h1>
		<div><%-@content%></div>
		```

	3. A document at `src/documents/posts/hello.html.md` that contains:

		``` html
		---
		layout: post
		title: Hello World!
		---
		Hello **World!**
		```

1. Then generate your website by running `docpad run` and you will get a html file at `out/posts/hello.html` that contains:

	``` html
	<html>
		<head><title>Hello World!</title></head>
		<body>
		<h1>Hello World!</h1>
		<div>Hello <strong>World!</strong></div>
		</body>
	</html>
	```

1. Any files that are in `src/files` will be copied to the `out` directory. E.g. `src/files/styles/style.css` -> `out/styles/style.css`

1. Awesome. Now what was with the `<%=...%>` and `<%-...%>` parts which were substituted away?

	1. This is possible because we parse the documents and layouts through a template rendering engine. The template rendering engine used in this example was [Eco](https://github.com/sstephenson/eco) (hence the `.eco` extensions of the layouts). Templating engines allows you to do some pretty nifty things, in fact we could display all the titles and links of our posts with the following:

		``` erb
		<% for document in @documents: %>
			<% if document.url.indexOf('/posts') is 0: %>
				<a href="<%= document.url %>"><%= document.title %></a><br/>
			<% end %>
		<% end %>
		```

1. That makes sense... now how did `Hello **World!**` in our document get converted into `Hello <strong>World!</strong>`?

	1. That was possible as that file was a [Markdown](http://daringfireball.net/projects/markdown/basics) file (hence the `.md` extension it had). Markdown is fantastic for working with text based documents, as it really allows you to focus in on your content instead of the syntax for formatting the document!

1. Awesome! Thanks for that!
