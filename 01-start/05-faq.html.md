```
title: "FAQ"
```

## Does it work on Windows?

Sure does. [Install it now.](/docpad/install)


## What is markup?

Whenever we write something we're using markup. It's merely a way of formatting content. For instance, if we are writing a `.txt` file in Notepad, we will be using `plain-text` as the markup. But say we want to get more advanced, and add things like **bold** text or _italic_ text to our content, then we could use a markup like `Microsoft Word (.doc)`, `Rich Text Format (.rtf)` or simply `Markdown (.md)` or `HTML (.html)`. These markups allow us to express our content with rich formatting.

For instance, **bold** in Markdown is `**bold**`, where in HTML it is `<strong>bold</strong>`. The markup that you choose for your content is highly dependent on what content you'd like to write. If you're mostly dealing with structural data (like a page layout) then `HTML`, `Jade`, `Haml`, or `CoffeeKup` would be a good way to go. If you're mostly dealing with textual data (like a blog post) then `Markdown` would probably the way to go.

DocPad supports unlimited markups thanks to its plugin system. It doesn't believe in a one size fits all, but in always using the best tool for a job. It's easy to learn new markups, there may be a bit of a learning curve, but you'll quickly adjust, be empowered, and grateful that you now have a new tool under your belt.

DocPad currently only supports rendering plain-text formats, meaning that rendering binary formats like `img` to `jpg` or binary-text formats like `doc` to `rtf` (they're not plain-text formats like `txt`, `docx`, or `xml` but in fact binary formats) does not currently work. [We will be addressing this in a future release of DocPad.](https://github.com/bevry/docpad/issues/684)


## What is a templating engine?

Often at times we will write documents which start seeming a bit repetitive, or we would like to add a bit of dynamicness to our document. Templating engines allow us to do this, as they allow for the insertion of logic into our chosen markup.

For instance, if I wanted to display a random number I could do the following:

- [Eco][1]: `<%= Math.random() %>`
- [Jade][2]: `= Math.random()`
- [Haml][3]: `= Math.random()`

This is pretty useful, as we can also do things like loops, or assign certain pages or parts of our layout into new files and use them again and again whenever we need them, instead of having to manually duplicate content. This is what empowers us to be able to use Layouts - discussed next.


## What is a layout?

Layouts wrap over our documents. They are generally the most generic and re-used part of an entire website, or book for that matter. They contain generally the layout of the page, including the structural information and the meta information (used for search engines, etc.).


## What is a document's meta information/data?

At the start of each document is an optional area right up the top that looks something like this

``` html
---
title: "My awesome blog post"
---
```

That is your document's meta data. It won't be included in the output of the document. You can use it to assign extra data to your document such as title, date, tags, etc.


## Is a document aware of its meta data?

It sure is! 

If you're using Eco as the rendering engine, you can totally do this:

``` html
---
title: My awesome blog post
meaningOfLife: 42
---

What is the meaning of life? <%= @document.meaningOfLife %>
```

To use Eco, simply ensure that you have the extension `.eco` at the end of your file (e.g., `my-blog-post.html.eco`). It doesn't have to be at the end, but it mustn't be the first extension (as the first extension is what you are rendering to).


## What do the extensions mean?

The extensions `.html.eco` means process this with Eco and render it as HTML. Alternatively, we can get pretty inventive and do something like this: `.html.md.eco` which means process this with Eco, then Markdown and finally render it as HTML.


## What is `findAllLive`?

DocPad's querying capabiliites are provided by a project called [Query-Engine](http://github.com/bevry/query-engine) which adds support for NoSQL queries to JavaScript Objects and Backbone Collections. In DocPad's case, we use Backbone for our Models, so we enhance our collections with Query-Engine to gain NoSQL querying for them.

There are two methods that Query-Engine provides for querying Backbone Collections. The first is `findAll` and the second is `findAllLive`.

`findAll` does a once-off scan of all the models in the collection that matches the criteria and returns the result in a new Backbone Collection, pretty standard stuff.

`findAllLive` creates a new child collection with the original collection as the parent, the new child collection then listens to the change events of the parent, and will automatically test the changes against the child collection's criteria. This is incredibly effecient for long running collections which data changes over time.

Never use `findAllLive` for short-lived collections (especially in your templates). It will cause more and more and more child collections and listeners to be created and added, causing a memory leak and unexpected results.


## Which one should I use and when?

Use `findAllLive` when defining long-running custom collections. Usual use cases are via the `collections` property of your [docpad configuration file](/docpad/config), or via the [`extendCollections` event](/docpad/events#extendcollections) within your plugin.

Use `findAll` when you are needing once-off/short-living collections. Usual use cases are inside your templates, or inside other events within your plugin.

However, ideally wherever possible you should try and use DocPad's built-in [template helpers](/docpad/template-data#querying) or [APIs](/docpad/api#querying) for querying as these methods are highly optimised for DocPad, which the low-level Query-Engine methods are not.


## How can I learn more about the NoSQL queries available and the internals of Query-Engine?
[Take a look at the Query-Engine Using Guide](https://github.com/bevry/query-engine/wiki/Using)


## How do I hide a document from being rendered (e.g., a draft post)? 

Check out the `ignored` [meta data property](/docpad/meta-data).


## How do I re-render a document on each request (e.g., dynamic documents)?

Check out the `dynamic` [meta data property](/docpad/meta-data).


## What are render passes?

Rendering is a multi-step process. First we render everything that is a standalone document (i.e. documents that don't including anything else). Once that is done, we then render all documents that include other documents. This is useful, as we can first render blog posts, then render the content listings second.

At times, you may have multiple levels of cross document references. For instance if document a references document B which references document C. In this case you would want to up the `renderPasses` configuration option for each amount of cross document references you have.


## How do I create custom 404 and 500 pages?

Add a `src/documents/404.html` for 404 pages, and `src/documents/500.html` for 500 pages. If you create a dynamic page (adding the `dynamic: true` meta data header) your templating engine (e.g., `404.html.eco`) will also get access to `req` (the request instance), `res` (the response instance), `err` (the error that occured - for 500 errors pages only, not for 404 error pages). Allowing you to do something like this for `src/documents/500.html.md.eco`:

```
---
layout: default
title: "An internal error occured - 500"
dynamic: true
---

## An error occured on <%= @req.url %>: <%= @err.message %>
```


## What data is exposed to my template engine?

Templating engines are renderers for languages which support business logic. For instance, the template engine [Eco](https://github.com/sstephenson/eco) provides us with the following syntax `<% your business logic %>` or to output a variable we can use `<%=some variable%>`.

As such, the data which we expose to our templating engines is called the `templateData`. [Check out the full listing of template data & helpers here.](/docpad/template-data)

For instance, to output the current document's title with Eco, you would use: `<%=@document.title%>`. The reason for the `@` is because Eco associates the `templateData` to the current scope, which with CoffeeScript (what Eco uses) you access by using the `@` character.


## How can I use environment variables in DocPad?

All environment variables are automatically available in Node applications through [`process.env`](http://nodejs.org/api/process.html#process_process_env). DocPad also loads varibles from a special [environment file](/docpad/config#environment-configuration-file). 

To quickly override existing environment variables for a single invocation of DocPad, specify it on the command line before the `docpad` command:
```
$ API_URL=localhost:1234 docpad run
```


## How do I disable certain plugins?

Check out the `enabledPlugins` [configuration property](/docpad/config).


## How do I only enable the plugins that I actually use?

Check out the `enableUnlistedPlugins` [configuration property](/docpad/config).


## How do I customise the configuration sent to a plugin?

Check out the `plugins` [configuration property](/docpad/config).


## Where can I host my DocPad website?

[Check out our deployment section here.](/docpad/deploy)


## How can I get Jade to render other DocPad supported markups?

[Check out the usage section on the Jade Plugin.](https://github.com/docpad/docpad-plugin-jade#usage)


## How can I get my templating engine to render other DocPad supported markups?

[Check out the text plugin.](/plugin/text/)


## How can I re-use particular templates again and again throughout my site?

[Check out the partials plugin.](/plugin/partials/)


## How do I make DocPad detect file changes faster?

Check this [GitHub issue](https://github.com/bevry/docpad/issues/749), see if it helps. :)


## Cannot get past accepting the Terms of Service

Check this [GitHub issue](https://github.com/bevry/docpad/issues/854) for a conversation on this bug.

TL;DR start DocPad with the `--offline` option and see if that works. :)


## Want more help?

- Getting errors? [Try our Troubleshooting Page](/docpad/troubleshoot)
- Need support? [Check out our Support Channels](/support)

[1]: https://github.com/sstephenson/eco  "Eco"
[2]: http://jade-lang.com                "Jade"
[3]: http://haml.info                    "Haml"
