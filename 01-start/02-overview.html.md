```
title: "Overview"
```
## Standard Project Structure

Here is the standard project structure you'll see in DocPad projects:

- `my-website/`
	- `out/`
	- `src/`
		- `render/` (also `documents/`, for backwards compatability)
		- `static/` (also `files/`, for backwards compatability)
		- `layouts/`
	- `docpad.coffee`
	- `package.json`

### The `out` Directory

This directory contains anything that DocPad generates. Any new files added to the `src` directory will be found here after being rendered and written by DocPad. However any files that are deleted from the `src` directory will not be deleted from the `out` directory by DocPad, you have to delete them manually. So if you remove a file and it's still there remember to delete it manually. ;-)


### The `src` Directory

This directory contains your website's source files. It contains your layouts, files to be rendered and be in the output and files that are not to be rendered but will still be in the output. The `src` can have the following folders:

- The `layouts` directory
- The `render` directory (also `documents`, for backwards compatability)
- The `static` directory (also `files`, for backwards compatability)

The `render` and `documents` directories, and the `static` and `files` directories, are merged; files appearing in either are rendered or copied to the output. However, you should use the former names rather than the latter to conform with the latest naming conventions.



#### The `layouts` Directory

Layouts work in a very similar way to files in `render`, in that they are rendered and they support meta data. Unlike the files in `render`, however, they are not output to the `out` directory, as they only exist to wrap files in `render` and other layouts within themselves. Layouts work in a nested fashion, with the desired layout being defined by the `layout` meta data property within the child layout/document.

Layouts should include child content, which is done using the `content` [template data](/docs/template-data#standard-template-data) variable. For instance, the code to use the content variable with the [Eco](https://github.com/sstephenson/eco/) templating engine via the [Eco DocPad plugin](https://github.com/docpad/docpad-plugin-eco) would be `<%- @content %>`.


#### The `render` Directory

These are files that we would like to render. Rendering occurs extension to extension in the same way the Ruby on Rails asset pipeline works. This means the document `src/render/hello.ext1.ext2.ext3` is rendered from `ext3` to `ext2`, then from `ext2` to `ext1`, resulting in the file `out/hello.ext1`. More common examples of this are rendering [CoffeeScript](http://coffeescript.org) to JavaScript with the document `src/render/script.js.coffee` to `out/script.js` or writing a blog post that renders from [Markdown](http://daringfireball.net/projects/markdown/) to HTML with the document `src/render/blog/hello.html.md` to `out/blog/hello.html`.

The reason we do not support direct rendering from `script.coffee` to `script.js` is that such a convention would eliminate the ability to combine extension renderings, also because ambiguity between extensions that can be rendered in multiple ways. For instance the `coffee` extension could be rendered using [CoffeeScript](http://coffeescript.org) to JavaScript or using [CoffeeKup](http://coffeekup.org) to HTML. However, if you really want to use just a single extension, such a thing is supported by the `renderSingleExtensions` meta property.

The other important aspect of files in `render` it that they support meta data. Meta data goes at the top of a document and defines information about that particular document. For instance, its title, date and layout are good examples. Meta data is not restricted to particular values, meaning you can define whatever meta data you want against a document. There are some special meta data properties, however, that perform certain functions (e.g., `layout` is used to specify the layout that should be used to wrap the document). You can find the complete listing of special meta data properties on the [Meta Data page](/docs/meta-data).


#### The `static` Directory

Files in this folder, like those in `render`, are output to the `out` directory. The difference lies in that they are not rendered and do not support meta data. This is where you should put everything that doesn't need to be rendered or need meta data. For example, images, vendor files, plain stylesheet and JavaScript files, etc.


### The `docpad.coffee` file

The `docpad.coffee` file can have several different extensions. It defines DocPad's settings. You can find full documentation on the [Configuration docs page](/docs/config).


### The `package.json` File

This file is needed for every Node.js application. It defines the dependencies that your application requires, such as the DocPad version that your site is developed with and the plugins you are running. You can learn more about `package.json` files on [this page](/node/ecosystem) of our [Hands on Node Training](/node/preface).
