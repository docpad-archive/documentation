### Does it work on windows?
Sure does, check the installation instructions in the [Readme](https://github.com/bevry/docpad).


### What is markup?
Whenever we write something we are using markup :-) It's merely a way of formatting content. For instance, if we are writing a .txt file in notepad, we will be using `plain text` as the markup. But say we want to get more advanced, and add things like **bold** text or _italic_ text to our content, then we could use a markup like `Microsoft Word (.doc)`, `Rich Text Format (.rtf)` or simply `Markdown (.md)` or `HTML (.html)`. These markups allow us to express our content with rich formatting.

For instance, **bold** in Markdown is `**bold**`, where in HTML it is `<strong>bold</strong>`. The markup that you choose for your content is highly dependent on what content you'd like to write. If you're mostly dealing with structural data (like a page layout) then `HTML`, `Jade`, `HAML`, or `CoffeeKup` would be a good way to go. If you're mostly dealing with textual data (like a blog post) then `Markdown` would probably the way to go.

DocPad supports a true series of markups for your project, it doesn't believe in a one size fits all, but the best tool for a job. Always use the best markup for the job, even if it may be a bit of a learning curve, you'll quickly adjust and be empowered and grateful you did :-)


### What is a templating engine?
Often at times we will write documents which start seeming a bit repetitive, or we would like to add a bit of dynamicness to our document. Templating engines allow us to do this, as they allow for the insertion of logic into our chosen markup.

For instance, if I wanted to display a random number I could do the following:

- Eco: `<%= Math.random() %>`
- Jade: `#{Math.random()}`
- HAML: `= Math.random()`

This is pretty useful, as we can also do things like loops, or assign certain pages or parts of our layout into new files and use them again and again whenever we need them, instead of having to manually duplicate content. This is what empowers us to be able to use Layouts - discussed next.


### What is a layout?
Layouts wrap over our documents. They are generally the most generic and re-used part of an entire website, or book for that matter. They contain generally the layout of the page, including the structural information and the meta information (used for search engines etc).


### What is a document's meta information/data?
At the start of each document is an optional area right up the top that looks something like this

```
---
title: "My awesome blog post"
---
```

That is your document's meta data. It won't be included in the output of the document, and is where you can assign extra data to your document such as title, date, tags, etc.


### Is a document aware of it's meta data?
It sure is, if you are using eco as the rendering engine, you can totally do this:

``` html
---
title: "My awesome blog post"
meaningOfLife: 42
---

What is the meaning of life? <%= @document.meaningOfLife %>
```

To use eco, simply ensure that you have the extension `.eco` at the end of your file. E.g. `my-blog-post.html.eco`. It doesn't have to be at the end, but it mustn't be the first extension (as the first extension is what you are rendering to).


### What do the extensions mean?
The extensions `.html.eco` means process this with Eco and render it as HTML. Alternatively, we can get pretty inventive and do something like this: `.html.md.eco` which means process this with Eco, then Markdown and finally render it as HTML.


### How do I hide a document from being rendered? E.g. a draft post.
Add the following to your document's meta data

``` coffee
ignored: true
```


### How do I re-render a document on each request? E.g. dynamic documents.
Add the following to your document's meta data

``` coffee
dynamic: true
```


### What data is exposed to my template engine?
Templating engines are renderers for languages which support business logic. For instance, the template engine [Eco](https://github.com/sstephenson/eco) provides us with the following syntax `<% your business logic %>` or to output a variable we can use `<%=some variable%>`.

As such, the data which we expose to our templating engines is called the `templateData`, and it contains the following:

- `require`: a reference to node's [require](http://nodejs.org/api/globals.html#globals_require) function, use it to include other node modules on the fly
- `docpad`: a reference to the currently running DocPad instance which is rendering the document
- `database`: a [Query-Engine](https://github.com/bevry/query-engine) collection of all our documents
- `document`: a JavaScript Object containing the serialised values of our `documentModel` (e.g. `documentModel.toJSON()`)
- `documentModel`: a reference to the current document we are rendering, documents are defined by the [Document Class](https://github.com/bevry/docpad/blob/master/lib/models/document.coffee) which extends the [File Class](https://github.com/bevry/docpad/blob/master/lib/models/file.coffee) which extends a [Backbone Model](http://documentcloud.github.com/backbone/#Model)
- `documents`: an array of all the website's documents, sorted newest to last
- `site`: an object of several site-specific properties, contains:
    - `date`: a javascript date object for the time that the website was last generated
- `blocks`: an object that contains several properties relating to blocks to be inserted without our layout, contains:
    - `scripts`: an array of strings which should be outputted where your script elements go
    - `styles`: an array of strings which should be outputted where your style elements go
    - `meta`: an array of strings which should be outputted where your meta elements go
- `req`: dynamic documents will also have this available to the, it is a reference to the current request object created by the [ExpressJS](http://expressjs.com/) framework

For instance, to output the current document's title with eco, you would use: `<%=@document.title%>`. The reason for the `@` is because Eco associates the `templateData` to the current scope, which with CoffeeScript (what eco uses) you access by using the `@` character.


### How do I disable certain plugins?
Inside your website's `package.json` file, you can add a `"docpad": {}` property - it may already be there. Inside that property, add `"enabledPlugins": {}` and inside that, add the name of the plugin you want to disable followed by `false` - e.g. if we wanted to disable the `eco` plugin we would have:

``` javascript
{
	// ...
	"docpad": {
		"enabledPlugins": {
			"eco": false
		}
	}
}
```


### How do I only enable the plugins that I actually use?
Inside your website's `package.json` file, you'll want to set the property `docpad.enableUnlistedPlugins` to `false`. This will only load plugins which are explicitly set to true inside in the `docpad.enabledPlugins` property. E.g. to only the run eco and stylus plugins we would have:

``` javascript
{
	// ...
	"docpad": {
		"enableUnlistedPlugins": false,
		"enabledPlugins": {
			"eco": true,
			"stylus": true
		}
	}
}
```


### How do I customise the configuration sent to a plugin?
Inside your website's `package.json` file, you'll want to customise the property `docpad.plugins`. This property contains the configuration sent to all the different plugins. So for example, if we wanted to tell the stylus plugin that we don't want it to include nib, then we can do:

``` javascript
{
	// ...
	"docpad": {
		"plugins": {
			"stylus": {
				"useNib": false
			}
		}
	}
}
```


### Where can I host my docpad website?
[Check out the Hosting Guide here](https://github.com/bevry/docpad/wiki/Hosting)


### Where can I find guides and tutorials about DocPad?
[Check out the Guides Page here](https://github.com/bevry/docpad/wiki/Guides)




## Need more help?

- Getting errors? [Try troubleshooting](https://github.com/bevry/docpad/wiki/Troubleshooting)
- Found a bug? [File a Bug Report on the Github Issue Tracker](https://github.com/bevry/docpad/issues)
- Need support? [Post a message in our Google Group Community](https://groups.google.com/forum/#!forum/docpad)
