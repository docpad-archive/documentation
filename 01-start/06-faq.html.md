```
title: "FAQ"
```

## Does it work on windows?
Sure does. [Install it now.](/docpad/install)


## What is “markup”?
Whenever you write something, you’re using markup. It's merely a way of formatting content. 

For instance, if you’re writing a `.txt` file in Notepad, you’re using `plain text` markup. 

But if you want to get more advanced, and add things like **bold** text or _italic_ text to our content, you might use a different markup—like `Microsoft Word (.doc)`, `Rich Text Format (.rtf)`, or simply `Markdown (.md)` or `HTML (.html)`. These allow us to express our content with rich formatting.

For instance, **bold** in Markdown is `**bold**`, where in HTML it is `<strong>bold</strong>`. The markup that you choose for your content is highly dependent on what content you'd like to write. If you're mostly dealing with structural data (like a page layout) then `HTML`, `Jade`, `HAML`, or `CoffeeKup` would be a good choice. If you're mostly dealing with textual data (like a blog post) then `Markdown` is almost certainly the way to go.

DocPad supports a true series of markups for your project; it doesn't believe in a one-size-fits-all, but the best tool for the job. Always use the best markup for the job—even if it may be a bit of a learning curve, you'll quickly adjust, become empowered, and be grateful. :-)


## What is a templating engine?
Sometimes you’ll be writing documents that begin to get repetitive; or, you’d like to add a bit of dynamic-ness to your document. Templating engines allow us to do this, as they allow for the insertion of logic into our chosen markup.

For instance, if I wanted to display a random number, I could do the following:

- Eco: `<%= Math.random() %>`
- Jade: `#{Math.random()}`
- HAML: `= Math.random()`

This is pretty useful. You could also do loops, or assign certain pages (or parts of your layout), into new files; then you could use them again and again, wherever you need them, rather than having to duplicate content manually. This is what empowers us to be able to use Layouts (next).


## What is a layout?
Layouts “wrap” documents. They’re the most generic and reusable part of an entire website (or book, for that matter). They contain the overall layout of a page (including the structural information), as well as the meta data (used for search engines, etc.).


## What is meta data?
At the beginning of any document, there’s an optional area that looks something like this:

``` html
---
title: "My awesome blog post"
---
```

That the document's **meta data**. It's not included in the output of the document. You can use it to assign extra data to your document (like its title, date, tags...or anything you want, really).


## Is a document aware of its meta data?
It sure is! 

For example, if your rendering engine is eco, you can totally do this:

``` html
---
title: "My awesome blog post"
meaningOfLife: 42
---

What is the meaning of life? <%= @document.meaningOfLife %>
```

To use eco, simply ensure that you have the extension `.eco` in the filename (e.g. `my-blog-post.html.eco`). The `.eco` can be anywhere **except first** in the chain of file extensions.  (Remember: the first file extension is what the document will render **to**.)


## What do the extensions mean?
The extensions `.html.eco` means “process this with Eco, and render it as HTML”. 

Alternatively, you can get inventive and do something like this: `.html.md.eco`. That means “process this with Eco, *then* process the result with Markdown, and finally render it as HTML”.


## How do I hide a document from being rendered? (e.g., an article’s draft )
Check out the `ignored` [meta data property](/docpad/meta-data).


## How do I re-render a document on each request? (e.g. dynamic documents)
Check out the `dynamic` [meta data property](/docpad/meta-data).


## What are “render passes”?
Rendering is a multi-step process:

1. First, DocPad renders all standalone documents.  (That is to say, documents that don’t include anything from other files.) 
2. Next, DocPad renders all documents that include other documents. (These first two steps allow DocPad to do things like “render all blog posts first, then render list of blog posts second.)
3. Sometimes, documents reference each other *multiple* times. (For example, document *A* references document *B*, which references document *C*.) If this is the case, you’ll need to set up the `renderPasses` configuration option.  It should be set according to the number of cross-references in your documents.


## How do I create custom `404` and `500` pages?
Add a `src/documents/404.html` for `404` pages, and `src/documents/500.html` for `500` pages. 

If you create a dynamic page (`dynamic: true` is in the meta data header), your templating engine will also have access to the following: 

- `req`, the request instance)
- `res`, the response instance)
- `err`, the `500`-level error (for `500` errors pages only)

That allows you to do something like this for `src/documents/500.html.md.eco`:

```
---
layout: default
title: "An internal error occured - 500"
dynamic: true
---

## An error occured on <%= @req.url %>: <%= @err.message %>
```


## What data is exposed to my template engine?
Templating engines are renderers for languages that support business logic. For instance, the template engine [Eco](https://github.com/sstephenson/eco) allows the syntax `<% business logic %>`; or to print a variable: `<%= some variable %>`.

As such, the data exposed to your templating engine is called `templateData`. [Check out the full listing of template data and helpers here.](/docpad/template-data)

For instance, to output the current document's title (with eco): `<%= @document.title %>`. 

The `@` character is because Eco associates `templateData` with the current scope. Eco uses CoffeeScript, and CoffeeScript uses `@` to access the current scope. (This is the equivalent of Javascript’s `this`.)


## How can I use environment variables in DocPad?
All environment variables are automatically available in Node applications through [`process.env`](http://nodejs.org/api/process.html#process_process_env). 

DocPad also loads variables from a special [environment file](/docpad/config#environment-configuration-file). You can quickly override environment variables for a single DocPad command like so:
```bash
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


## How can I get jade to render other DocPad-supported markups?
[Check out the usage section on the Jade Plugin.](https://github.com/docpad/docpad-plugin-jade#usage)


## How can I get my templating engine to render other DocPad-supported markups?
[Check out the text plugin.](/plugin/text/)


## How can I reuse particular templates again and again throughout my site?
[Check out the partials plugin.](/plugin/partials/)


## Want more help?

- Getting errors? [Try our Troubleshooting Page](/docpad/troubleshoot)
- Need support? [Check out our Support Channels](/support)
