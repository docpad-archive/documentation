```
title: "Beginner Guide"
cssClasses: ['compact']
```

## Introduction

Welcome to the Beginner Guide for DocPad. By the end of this guide, you'll know how to create amazing powerful web sites and applications with DocPad. You won't need any special training. (And if you’re a web developer, you'll feel right at home.)

For this guide, we'll create a blog, step by step. In this guide, we’ll refer to both **posts** and **pages**.

- **Posts** are like status updates, or articles.  They might be archived, but you probably don’t want to show all of them, all the time.
- **Pages** are content that always shows.

Great! Lets get started. 

(Oh…and if you ever get stuck, have a question, or need help, [then jump onto any of our official support channels](/support), and we'll be right with you. Cheers!)










## Create a standard project structure

Before start any content, we’ll have to create a project and set it up with the [standard structure](/docpad/overview) that DocPad uses. 

To do this, run the following:

``` bash
mkdir my-new-website
cd my-new-website
docpad run
```

When prompted for a skeleton, select `No Skeleton`. That'll set up the standard directory structure for you automatically. 

The `docpad run` command will also *keep* running once the action has completed successfully. That’s because DocPad watches for changes, and regenerate your website when they occur. It also starts a web server on [http://localhost:9778](http://localhost:9778) so you can view your website as you go!

Allow `docpad run` to keep running for now. Whenever you want to stop it, hit `CTRL+C` to exit.


## Adding the Home Page

Let’s create our first document: our website’s homepage! 

Create `src/documents/index.html`, and give it the following content:

``` erb
<html>
<head>
	<title>Welcome! | My Website</title>
</head>
<body>
	<h1>Welcome!</h1>
	<p>Welcome to My Website!</p>
</body>
</html>
```

Once you've saved it, open [http://localhost:9778](http://localhost:9778) (or refresh, if you had it open already). You'll notice DocPad has already regenerated your website, and the page you created above is rendered in the browser. Fantastic!



## Adding the About Page and a Layout

Now, you'll want to add an “About Me” page so readers can know who you are! 

To do this, create `src/documents/about.html` and give it the content:

``` erb
<html>
<head>
	<title>About Me | My Website</title>
</head>
<body>
	<h1>About Me</h1>
	<p>I like long walks on the beach. <strong>Plus I rock at DocPad!</strong></p>
</body>
</html>
```

Now, if you go to [http://localhost:9778/about.html](http://localhost:9778/about.html), you'll see the page in our browser. Awesome!

But you know what’s *not* so awesome?  Duplicating that layout information from the homepage. For instance, if you wanted to change the contents of `<head>`, you’d have to change it in two places! 
    
This is where **layouts** come in. Layouts “wrap” around documents, and reduce this kind of redundancy. They define the *surrounding* areas of a document.  

So what you’ll do is move the wrapper stuff from your two documents into a new layout. 

Create `src/layouts/default.html.eco`, with the following:

- `src/layouts/default.html.eco`

	``` erb
	<html>
	<head>
		<title><%= @document.title %> | My Website</title>
	</head>
	<body>
		<h1><%= @document.title %></h1>
		<%- @content %>
	</body>
	</html>
	```

Now, you’ll need to tell your other documents to use the `default` layout:

- `src/documents/index.html`

	``` erb
	---
	title: "Welcome!"
	layout: "default"
	isPage: true
	---

	<p>Welcome to My Website!</p>
	```

- `src/documents/about.html`

	``` erb
	---
	title: "About Me"
	layout: "default"
	isPage: true
	---

	<p>I like long walks on the beach. <strong>Plus I rock at DocPad!</strong></p>
	```

But if you go to either page on the web server, it won’t work quite as you expect! It’s just the layout, but it’s not populated with the content. 

That’s because you haven't yet installed a templating engine for your new layout!  Don’t worry…you’ll fix that in just a second.

(Also note the addition of an `isPage` attribute to the documents. It’s a **custom** attribute; it has no special meaning to DocPad. DocPad lets you define *whatever* attributes you want, to use *however* you want.  You’ll come back to `isPage` in a bit, and tell DocPad how to behave when it sees `isPage` in your documents.)


### Installing the Templating Engine

Templating Engines allow us to embed *abstractions* inside documents. That’s why you use layouts. A layout is an *abstraction* that wraps a document and outputs its contents in a specific way.

For this guide, we’ll use the [eco](https://github.com/sstephenson/eco) templating engine. It’s available via the [eco plugin](/plugin/eco). 

Let’s install it now. First, quit DocPad (`CTRL+C`), then run:

``` bash
docpad install eco
```

Now run DocPad again (`docpad run`). When you visit your homepage or About page, you'll see that the page has been populated with the document’s content! 

In other words, it's actually rendered correctly, thanks to the eco templating engine! *w00t w00t!*


### To escape, or not to escape…

Sharp-eyed readers may have noticed something curious about the layout file… 

**Why does the document title use `<%=`, while the content uses `<%-`?**

Well eco, `<%=` escapes data before output, while `<%-` outputs data as-is. 

**So why should I escape some things, and not others?** 

Generally, whenever the data to output is HTML (i.e. document content), you probably want to output it as-is (without any escaping). Otherwise, it’s a good idea to escape the data before output. 

Why? Well, imagine the document title is `3 is > 2`. If you tried to output without escaping, you could end up with something like `<title>3 is > 2</title>`, which is invalid HTML (due to the `>`). But if you used escaped output, you  get `<title>3 is &gt; 2</title>`, which is valid HTML (and will still look correct to the user).


### A note on Plugins

Although you used the eco templating engine in this guide, there are plenty of others you can use, too! 

We think eco is the most beginner-friendly, as it’s the most like HTML. However, after experimenting with some others, you may prefer to use them instead. Adding support for a new templating engine (or pre-processor, or whatever) is as simple as installing the plugin for it.

But DocPad also supports more than just templating engines. It has a whole range of plugins for all sorts of different things. So be sure to check out everything we've got [on the Plugins page](/docpad/plugins).


### A note on Rendering

DocPad can support multiple templating engines because of how it renders things: extension by extension. 

So, by doing `src/layouts/default.html.eco`, DocPad renders from eco to html, due to the order of the extensions. 

Now, if we tried something like `default.eco.html`, it would signal DocPad to try rendering from `html` → `eco`, which isn't possible. But things like CoffeeScript → JavaScript are quite possible. (You could also do JavaScript → CoffeeScript.) Basically, if DocPad has the appropriate plugin, it will render it.

You can also mix and match extensions. By doing something like `default.html.md.eco`, DocPad renders from eco → markdown → html. That would let you use eco abstractions in your markdown documents. Awesome!  

(But I digress…way out of our scope. So let’s get back on track!)


### A note on Meta Data

The stuff between `---` at the top of documents is **meta data**.  It’s where you can define extra information about your document—such as title, layout, date, or whatever else you can think of.  It's up to you.  

There are a few pre-defined properties (like `layout`, which we just used).  Other than that, there’s no limitations on the properties you can use.

[You can learn more about meta data and all the special properties on the Meta Data Page.](/docpad/meta-data)


## Adding the Live Reload Plugin and Blocks

### Adding the Live Reload Plugin

Sweet. So far, so good: we've got two documents, and a layout to abstract them. 

But as we make changes, it sure would be nice if we didn’t have to refresh our browser each time.  

Fortunately, there’s a plugin that can refresh the browser automatically!  Behold: the fabulous [live reload plugin](/plugin/livereload)! 

Let’s install it!

``` bash
docpad install livereload
```

But the next time you use `docpad run`, the browser still won’t refresh automatically! What gives? 

Relax. You just need to add your **Blocks**.

### Adding the Blocks

**Blocks** are a way for plugins (or even *you*) to be able to easily add scripts, styles and meta elements to pages. 

In the case of the LiveReload plugin, it needs the a script block in order to inject the necessary scripts into the page.  Those scripts are what will enable the browser to automatically refresh whenever changes are made.

To add the three default blocks to your layout, update it like so:

``` erb
<html>
<head>
	<title><%= @document.title %> | My Website</title>
	<%- @getBlock("meta").toHTML() %>
	<%- @getBlock("styles").toHTML() %>
</head>
<body>
	<h1><%= @document.title %></h1>
	<%- @content %>
	<%- @getBlock("scripts").toHTML() %>
</body>
</html>
```

Save your layout. Manually refresh your browser, so that it gets these changes. 

Now, your page has the LiveReload scripts injected, right where the scripts block gets output. 

**From now on, whenever you change any file in your DocPad project, the browser will automatically refresh.** Amazing!

In the next part, you'll work with blocks some more, by adding assets to them.












## Adding Assets

It's time to start adding some assets. But first, you should review [DocPad’s Overview Page](/docpad/overview); you’ll need to be familiar with the overall directory structure of a DocPad project.

Don’t worry.  I won’t go anywhere while you look it over.

…

Finished?  All right...let’s do this!


### Images

Let’s add our logo to your layout’s header. 

1. [Download the DocPad logo](http://d.pr/i/cfmt+)
2. Put it in the following location: `src/files/images/logo.gif` (binary files *always* go in `files/`) 
3. In your layout, add the following:

``` html
<img src="/images/logo.gif" />
```

(**Note:** If you’re downloading the file directory into the specified location, you may have to restart DocPad. Sorry about that.  We’re working on it!)


### Stylesheets

Next, let’s make your `h1` headers red. 

To do this, add `style.css` under `documents/styles/`.  Its contents should be:

``` css
h1 {
	color: red;
}
```

Now, to include it in your pages, update the `styles` block in your layout like so:

``` erb
<%- @getBlock("styles").add(["/styles/style.css"]).toHTML() %>
```

When you save the file, you’ll see the browser reload automatically. And your CSS file will be injected into the layout, making our header red!



### Scripts

Hmm...how about a nifty loading effect?  You can do this with a bit of JavaScript, thanks to the tools provided by JavaScript libraries (such as the oh-so-awesome [jQuery](http://jquery.com)). 

As always, you can use any JavaScript library you want. We’re just choosing jQuery for this guide. Let’s go:

1. [Download jQuery](http://code.jquery.com/jquery.js)
2. Move it to `src/files/vendor/jquery.js` 

The purpose of `files` directory is to contain files that you’re probably never going to want to render. Putting all of them in `files` is a good choice for consistency and speed. 

And, since you didn’t write jQuery yourself—unless you’re John Resig (Hi, John!)—it goes in `files/`**`vendor`**.

When it comes to your own scripts and styles, though, chances are you’ll render them with something. So, as a general guideline, put them in `documents/`.  It’ll make the transition to rendering engines easier, when your plans change in the future.  (And whose won’t?)

Now that you’ve got jQuery, add your nifty loading effect in a new file: `src/documents/scripts/script.js`. It should contain:

``` javascript
(function(){
	$("body").hide().fadeIn(1000);
})();
```

Cool.  Now, back in your layout, add those files to your scripts block:

``` erb
<%- @getBlock("scripts").add(['/vendor/jquery.js','/scripts/script.js']).toHTML() %>
```

Upon saving, you’ll notice that your content will fade in over a duration of two seconds. Nifty!

----

If you’re used jQuery before, you may have noticed that we omitted the [jQuery onDomReady](http://api.jquery.com/ready/) handler in our script file.  

Well, only code that requires the entire DOM to be loaded needs to go there. For example, if your script requires a DOM element that’s positioned after your script tag, that would require the entire DOM to be loaded. 

However, since DocPad injects scripts into the `body` element, they *already* have access to the `body`.  Therefore, the script can begin the `fadeIn` animation immediately. Otherwise, the script would wait for the entire page to load, then for the DOM to initialize, and *then* it would finally start the fade in. The extra wait time creates an undesired popping effect.

And nobody wants that.











## Getting the benefits of Pre-Processors
Pre-Processors are amazing things. They allow us to write documents in one language (the “source language”), but export them to a different language (the “target language”). 

This allows you to write code in a much friendlier syntax, instead of restricting you to the syntaxes that browsers expect.  But more importantly, pre-processors often provide powerful features that don’t exist in the target language, allowing you to code with powerful tools while still producing the older languages that browsers understand.


### Using Markdown, a HTML Pre-Processor
Open the About page you created earlier (`documents/about.html`). 

HTML’s verbose syntax is cumbersome for writing content that’s more text than markup (e.g. articles, comments, etc.). Fortunately, [Markdown](http://daringfireball.net/projects/markdown/) ([one of many HTML pre-processors available](/docpad/plugins)) comes to the rescue!

With Markdown, you can update your About page to the following:

``` markdown
I like long walks on the beach. **Plus I rock at DocPad!**
```

**This will produce the same result.**

But remember: as with all rendering engines, you’ll need to:

1. **Indicate the rendering we want to perform.** Rename `about.html` to `about.html.md`.
1. **Install the renderer plugin.** Run `docpad install marked` to install the [Marked Markdown Plugin](/plugin/marked).

Sweet. Now you’re now ready to rock the house with Markdown.


### Using Stylus, a CSS pre-processor
Open the stylesheet document you created earlier (`documents/styles/style.css`). 

CSS really hasn’t come that far over the years. It has absolutely no abstractions, making it incredibly redundant and painful to write. Fortunately, [Stylus](http://learnboost.github.com/stylus/) ([one of many CSS pre-processors available](/docpad/plugins)) comes to the rescue!

With Stylus, you can update your stylesheet to the following:

``` stylus
h1
	color: red
```

**This will produce the same result.** 

But remember: as with all rendering engines, you’ll need to:

1. **Indicate the rendering we want to perform.** Rename `style.css` to `style.css.styl`.
1. **Install the renderer plugin.** Run `docpad install stylus` to install the [Stylus Plugin](/plugin/stylus).

Sweet. Now you’re now ready to rock the house with Stylus.


### Using CoffeeScript, a JavaScript Pre-Processor
Open the JavaScript document we created earlier (`documents/scripts/script.js`). 

Sometimes, people get annoyed with JavaScript's verbosity. Sometimes they get *very* annoyed their entire app breaks because they forgot a comma somewhere. Fortunately, [CoffeeScript](http://coffeescript.org/) ([one of many JavaScript pre-processors available](/docpad/plugins)) comes to the rescue!

With CoffeeScript, you can update your script to the following:

``` coffeescript
$("body").hide().fadeIn(1000)
```

**This will produce the same result.** 

But remember: as with all rendering engines, you’ll need to:

1. **Indicate the rendering we want to perform**. Rename `script.js` to `script.js.coffee`.
1. **Install the renderer plugin.** Run `docpad install coffeescript` to install the [CoffeeScript Plugin](/plugin/coffeescript).

Sweet. Now you’re ready to rock the house with CoffeeScript.











## Adding some Template Data and Template Helpers using a Configuration File

### Purpose of a Configuration File

The [DocPad Configuration File](/docpad/config) allows you to configure your DocPad instance, listen for events, and perform some nifty abstractions.

Consider the case where your document title is empty. Currently, your page’s title would be ` | My Website`...in which case, it would be preferable simply to say `My Website` when the document doesn't have a title.

You can update your title code in the layout template to:

``` erb
<title><%= if @document.title then "#{@document.title} | My Website" else "My Website" %></title>
```

That will do the trick. But then you’d have to update the site’s title in *two* places, if you want to use something besides `My Website`. Since this is a pretty common abstraction, it would be nice if we could put it into some sort of central location…

Like a **configuration file**!

Create the configuration file `my-new-website/docpad.coffee`, with the following content:

``` coffee
# Define the Configuration
docpadConfig = {
	# ...
}

# Export the Configuration
module.exports = docpadConfig
```

You’ll need to restart DocPad, so that it sees configuration file. Thereafter, DocPad will automatically reload your configuration when changes occur.

The first part of the file is where you’ll define configuration itself (where the `# ...` is located). The second part is a [node convention](http://nodejs.org/docs/latest/api/modules.html#modules_module_exports) for exporting data from one file to another. 

Whenever you see “add some configuration”, it means “add it to the `docpadConfig` object”, which you just defined.

For more information on configuration files and their options, see [Configuration Page](/docpad/config).


### Using TemplateData for Abstractions

Everything available to templates is called [TemplateData](/docpad/template-data). For example, `@document` is part of our template data. So, to be able to abstract something for your templates to use, you’ll need to extend your template data. 

You can do this by modifying your template data configuration property, like so:

``` coffee
docpadConfig = {
	# ...
	templateData:
		site:
			title: "My Website"
	# ...
}
```

Your website title is now abstracted out.  Simple, wasn’t it?

Now, update the `title` element in your template to:

``` erb
<title><%= if @document.title then "#{@document.title} | #{@site.title}" else @site.title %></title>
```

From now on, you can change the title of your site in your configuration, and it will update across your entire site.  

But that’s just a string of text. You can take this (or any) abstraction even further, by putting it into a **function** under `templateData`.  That way, your abstractions can include **logic**!


### Abstracting Logic into Template Helpers

When using `.coffee` or `.js` files for your configuration, you can define functions. That way, you can use those functions in your `templateData`. 

These functions are known as **Template Helpers**.

A template helper’s scope is the same as wherever it’s called from. This makes abstracting out logic really really easy. 

Let’s see what it would look like:

``` coffee
docpadConfig = {
	# ...
	templateData:
		site:
			title: "My Website"

		getPreparedTitle: -> if @document.title then "#{@document.title} | #{@site.title}" else @site.title
	# ...
}
```

And your template becomes cleaner:

``` erb
<title><%= @getPreparedTitle() %></title>
```

Now *that’s* awesome. 

While this was a simple example, you can use this to do some truly cool stuff. For instance, [here’s an example that localize dates into French](https://gist.github.com/4166882)!

If you’re writing a plugin, you can use [the extendTemplateData event](/docpad/events) to extend the `templateData`.











## Adding a Menu Listing for our Pages

Remember your About page? 

Wouldn’t it be nice if, when you added pages, your menu updated automatically? 

It sure would. :) 


### Updating our Layout

Open your `default` layout (`src/layouts/default.html.eco`). 

Before the `h1`, add the following:

``` erb
<ul>
	<% for page in @getCollection("html").findAll({isPage:true}).toJSON(): %>
		<li class="<%= if page.id is @document.id then 'active' else 'inactive' %>">
			<a href="<%= page.url %>">
				<%= page.title %>
			</a>
		</li>
	<% end %>
</ul>
```

Bang! Now you’ve got a navigation menu on every page! 

Wicked. :D 

So, what’s happening here?

1. First, it uses the `getCollection()` [template helper](/docpad/template-data) to fetch the `html` collection. (The `html` collection is a pre-defined collection by DocPad; it contains all the HTML documents in your site.) 
2. Using that collection, DocPad finds everything where the `isPage` attribute set to `true`. (Remember `isPage`? You defined it earlier, when first applied a layout to your pages.) 
3. DocPad then converts the results from a [Backbone](http://backbonejs.org/#Collection)/[QueryEngine](/queryengine/guide) Collection into a standard JavaScript `Array` (using [`toJSON()`](http://backbonejs.org/#Collection-toJSON)).

That might seem overwhelming at first, but give it a while. You’ll be a pro in no time. 

There’s one major inefficiency with the above approach. Can you guess where?

In the above code, the query is run *every time* DocPad renders a layout. That’s a bit silly, since that query’s results aren’t going to change between renders. So, really, you only need to query it *once*, and then provide your collection with the results. 

Good thing you can.  Read on.


### Creating Custom Collections via the Configuration File

Go back to your [DocPad Configuration File](/docpad/config) (`docpad.coffee`). 

This time, add the following:

``` coffee
docpadConfig = {
	# ...
	collections:
		pages: ->
			@getCollection("html").findAllLive({isPage:true})
	# ...
}
```

Then inside your Default layout, update `getCollection` to:
	
``` erb
<% for page in @getCollection("pages").toJSON(): %>
```

Much better...and *way* more efficient. 

Did you spot the difference with the call we used? In the query, the new code used the method `findAllLive()` instead of `findAll()`. 

That’s because `findAllLive` utilizes [QueryEngine’s Live Collections](/queryengine/guide), which means that you only define your criteria *once*, and your collection is kept up to date over time. 

To get a bit more technical, this works by creating a live child collection of the parent collection. (In this case, the `html` collection is the parent, and `pages` is the child.) The child collection then subscribes to the parent collection’s `add`, `remove`, and `change` events, and tests the event’s model against the child’s criteria. If it passes, the collection adds it; if not, it removes it. 

This is a tremendous improvement over querying *everything*, *every* single time.

----

What about sorting? That’s easy enough. 

You can sort by adding a second argument to `@getCollection('html').findAllLive({isPage:true})`.  This will be** the  sorting argument**: `@getCollection('html').findAllLive({isPage:true},[{filename:1}])` 

In this case, you’ll sort by filename in ascending order. (To do descending order, change `1` to `-1`.) 

Now you can sort by *any* attribute available on your models. That means you could even add an `order` attribute to our document meta data, and sort using that, if you like. 

(**Note:** There’s also a third parameter, for **paging**. To learn more, including what kinds of queries are available, refer to the [QueryEngine Guide](/queryengine/guide).)


### Setting Default Meta Data Attributes for our Pages

Considering you’d probably like all your pages to use the `default` layout, you might make all pages use it without having to add `layout: default` to the [meta data](/docpad/meta-data) for every single one. 

Here’s how:

``` coffee
docpadConfig = {
	# ...
	collections:
		pages: ->
			@getCollection("html").findAllLive({isPage:true}).on "add", (model) ->
				model.setMetaDefaults({layout:"default"})
	# ...
}
```

What’s happening here? 

It’s the same as before—but this time you used the `add` event, which is automatically fired by [backbone](http://backbonejs.org/#Collection-add) whenever a model (a page/file/document/whatever) gets added to your collection. 

Inside the `add` event, you told DocPad “set the default meta data attributes for the model!”. Specifically, to set the layout’s default value to `"default"`.

This is priceless when doing more complicated things. For instance, we use it in this documentation, in order to be able to base the navigation structure of the documentation files from their physical location on the file system. 

For instance, if we have the file `docs/docpad/01-start/04-begin.html.md`, from the file’s path, we do the following: 

- we can detect that the project is `docpad`, so we assign `project: "docpad"` to the meta data
- the section is `start`, and it’s first in order, so we set `category: "start"` and `categoryOrder: 1`
- finally, the file is `begin`, and it’s 4<sup>th</sup> in order

That's just one example. There’s plenty more you’ll discover on your own epic journey!











## Adding Blog Posts

You now have all the tools and knowledge required to create the blog section! 

We’ve left this as an exercise for you. Use what you’ve learned, and the exercise will help you to retain the knowledge you’ve just gained.

If you need a few pointers to help get started, here you go:

- Create a new layout called `post` that uses the `default` layout, and use it to perform custom styling for your blog posts (e.g. `<div class="post"><%- @content %></div>`)
- When writing a blog post, give them a `date` meta data attribute (in the format of `date: 2012-12-25`), so you can sort them in reverse-chronological order
- Create a new directory called `posts` to contain all your blog posts, and use the query `relativeOutDirPath: 'posts'` for your custom collection to get all documents inside the `posts/` output directory (`/my-new-website/out/posts/`). 
- Create a new page called `posts.html.eco` to list all your blog posts. This will be more-or-less the same as your navigation menu. If you want to display descriptions for each post, just add a meta data attribute for blog posts, and output it. 
- If you want to show the rendered content of that data, try `post.contentRenderedWithoutLayouts()`.

(You can refer to the [Meta Data Page](/docpad/meta-data) for more information about what attributes are already available to you.)

- If you’re still stuck and need help, just hop on over to our [IRC Support Channel (docpad on freenode)](http://webchat.freenode.net/?channels=docpad) and someone will be with you soon enough :) [You can also discover all of our available Support Channels via our Support Page.](/support)

And, by the way: Congratulations! 

You now possess all the foundations required to be able to write amazing and powerful web applications (like those already in our [showcase](/docpad/showcase)). 

To recap, you learned how to:

- write documents in any language, markup, pre-processor, templating engine—whatever you wish—by installing the necessary plugin and changing the file’s extensions
- perform powerful abstractions using layouts, meta data, template data, and configuration files
- create incredibly efficient custom collections, filtered and sorted by your own criteria
- create your own custom listings of content

But it doesn’t stop here. These were just the foundations. If you can think it, you can do it with DocPad. Really, there are no limits with DocPad. That's why DocPad sets you free.

Farewell!










## Deployment

[Deployment is the next page of this guide.](/docpad/deploy)
