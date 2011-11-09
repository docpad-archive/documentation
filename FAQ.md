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

    ---
    title: "My awesome blog post"
    ---

That is your document's meta data. It won't be included in the output of the document, and is where you can assign extra data to your document such as title, date, tags, etc.


### Is a document aware of it's meta data?

It sure is, if you are using eco as the rendering engine, you can totally do this:

    ---
    title: "My awesome blog post"
    meaningOfLife: 42
    ---

    What is the meaning of life? <%= @document.meaningOfLife %>

To use eco, simply ensure that you have the extension `.eco` at the end of your file. E.g. `my-blog-post.html.eco`. It doesn't have to be at the end, but it mustn't be the first extension (as the first extension is what you are rendering to).


### What do the extensions mean?

The extensions `.html.eco` means process this with Eco and render it as HTML. Alternatively, we can get pretty inventive and do something like this: `.html.md.eco` which means process this with Eco, then Markdown and finally render it as HTML.


### How do I hide a document from being rendered? E.g. a draft post.

Add the following to your document's meta data

    ignored: true


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

Inside your website's `package.json` file, you'll want to set the property `docpad.enableUnlistedPlugins` to `true`. This will only load plugins which are explicitly set to true inside in the `docpad.enabledPlugins` property. E.g. to only the run eco and stylus plugins we would have:

``` javascript
{
	// ...
	"docpad": {
		"enableUnlistedPlugins": true,
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

### Does it support client-side editing of documents?

It sure does. Checkout `/nifty/client-side-editing.html` in the [kitchensink skeleton](https://github.com/balupton/kitchensink.docpad) for a demo :-)



### What is the list of properties on the default Document object?

Here's a list of what you'll have on the `Document` object that is passed into a template (unless you've added your own :P):

* fullPath
* relativePath
* extensions
* tags
* relatedDocuments
* date
* basename
* extension
* extensionRendered
* filename
* content
* contentSrc
* contentRaw
* contentRendered
* relativeBase
* title
* slug
* id
* url
* layout

### Does it work on windows?

[It's work in progress, but you can try this guide here](https://github.com/balupton/docpad/wiki/Windows-Installation)


### Where can I host my docpad website?

[Check out the Hosting Guide here](https://github.com/balupton/docpad/wiki/Hosting)


### Where can I find tutorials about DocPad?

[Check out the Tutorials Page here](https://github.com/balupton/docpad/wiki/Tutorials)


