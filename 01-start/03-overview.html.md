```
title: "Overview"
```


## Standard Project Structure

Here is the standard project structure you'll see in DocPad projects:

- `my-website/`
	- `out/`
	- `src/`
		- `documents/`
		- `files/`
		- `layouts/`
	- `package.json`


### The Documents Directory

Documents are files that we would like to render. Rendering occurs extension to extension in the same way the ruby on rails asset pipeline works. This means the document `src/documents/hello.ext1.ext2.ext3` is rendered from `ext3` to `ext2`, then from `ext2` to `ext1`, resulting in the file `out/hello.ext1`. More common examples of this are rendering [CoffeeScript](http://coffeescript.org/) to JavaScript with the document `src/documents/script.js.coffee` to `out/script.js` or writing a blog post that renders from [Markdown](http://daringfireball.net/projects/markdown/) to HTML with the document `src/documents/blog/hello.html.md` to `out/blog/hello.html`.

The reason we do not support direct rendering from `script.coffee` to `script.js` is that such a convention would eliminate the ability to combine extension renderings, as well as cause ambiguity between extensions that can be rendered in multiple ways. For instance the `coffee` extension could be rendered using [CoffeeScript](http://coffeescript.org/) to JavaScript or using [CoffeeKup](http://coffeekup.org/) to HTML. However, if you really want to use just a single extension, such a thing is supported by the `renderSingleExtensions` meta property.

The other important aspect of documents it that they support meta data. Meta data goes at the top of a document and defines information about that particular document. For instance, its title, date and layout are good examples. Meta data is not restricted to particular values, meaning you can define whatever meta data you want against a document. There are some special meta data properties, however, that perform certain functions (e.g. `layout` is used to specify the layout that should be used to wrap the document). You can find the complete listing of special meta data properties on the [Meta Data Page](/docpad/meta-data).


### The Layouts Directory

Layouts work in a very similar way to documents, in that they are rendered and they support meta data. Unlike documents, however, they are not output to the `out` directory, as they only exist to wrap documents and other layouts within themselves. Layouts work in a nested fashion, with the desired layout being defined by the `layout` meta data property within the child layout/document.

Layouts should include child content, which is done using the `content` [template data](/docpad/template-data) variable. For instance, the code to use this variable with the [Eco](https://github.com/sstephenson/eco/) templating engine via the [Eco Plugin](/plugin/eco) would be `<%- @content %>`.


### The Files Directory

Files are like documents, in that they are output to the `out` directory. The difference lies in that they are not rendered and do not support meta data. This is where you should put everything that doesn't need to be rendered or need meta data. For example, images, vendor files, plain stylesheet and javascript files, etc.


### The `package.json` File

This file is needed for every node application. It defines the dependencies that your application requires, such as the DocPad version that your site is developed with and the plugins you are running. You can learn more about `package.json` files on [this page](/node/ecosystem) of our [Hands on Node Training](/node/preface).
