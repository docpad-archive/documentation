```
title: "Overview"
```


## Standard Project Structure

Here’s the standard DocPad project structure:

- `my-website/`
	- `out/`
	- `src/`
		- `documents/`
		- `files/`
		- `layouts/`
	- `package.json`


### The Documents Directory

Documents are files you want rendered. Rendering occurs *extension to extension* (similar to how Ruby on Rails’ asset pipeline works). This means the document `src/documents/hello.ext1.ext2.ext3` is rendered from `ext3` → `ext2`, then from `ext2` → `ext1`, resulting in the file `out/hello.ext1`. 

More common examples include rendering [CoffeeScript](http://coffeescript.org/) to JavaScript (`src/documents/script.js.coffee` → `out/script.js`), or, rendering a blog post from [Markdown](http://daringfireball.net/projects/markdown/) to HTML (`src/documents/blog/hello.html.md` → `out/blog/hello.html`).

The reason DocPad doesn’t support rendering directly from `script.coffee` → `script.js` is that this would eliminate the ability to combine extension renderings. It would also cause ambiguity between extensions that may be rendered in multiple ways. (For instance, the `coffee` extension could be rendered using [CoffeeScript](http://coffeescript.org/) → JavaScript—**or**, using [CoffeeKup](http://coffeekup.org/) → HTML.) 

However, if you really want to use a single extension, this is is supported via the `renderSingleExtensions` meta property.

Which brings us to the other important thing about documents: they support **meta data**. Meta data goes at the top of a document, and defines information about that particular document (for example, a document’s `title`, `date`, and `layout`). 

Meta data isn’t restricted to particular values. You can define whatever meta data you want in a document. However, there are some special, pre-defined meta data properties, which perform certain functions; e.g. `layout` tells DocPad which layout to wrap a document with. 

You can find the complete listing of special meta data properties on the [Meta Data Page](/docpad/meta-data).


### The Layouts Directory

Layouts are similar to documents: they’re rendered, and they support meta data. 

However, unlike documents, they aren’t output to `out/`. They exist *only* to wrap documents (and other layouts) within themselves. 

Layouts work in a nested fashion, with the desired layout being defined by the `layout` meta data property, inside the child layout/document.

Layouts should include the child content. This is done with the `content` [template data](/docpad/template-data) variable. 

In the [Eco](https://github.com/sstephenson/eco/) templating engine (available via DocPad’s [Eco Plugin](/plugin/eco)),  you include child content like this: `<%- @content %>`.


### The Files Directory

Files are like documents, in that they’re output to `out/`. 

However unlike documents, they’re not rendered, and they don’t have meta data. Everything that doesn’t need to be rendered, and that doesn’t need meta data, should live under `files/`. 

Examples include images, vendor files, static stylesheets, and javascript, etc.


### The `package.json` File

This file is needed for every node application. It defines the dependencies that the application requires (like the DocPad version your site was created with—as well as the plugins you’re running), as well as other important stuff, too. 

You can learn more about `package.json` files on [the Node Ecosystem part](/node/ecosystem) of our [Hands-on Node Training](/node/preface).

