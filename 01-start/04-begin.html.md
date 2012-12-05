```
title: "Beginner Guide"
cssClasses: ['compact']
```

## Introduction

Welcome to the Beginner Guide for DocPad. By the end of this guide, you'll have all the knowledge necessary to create amazing powerful web sites and applications with DocPad. You won't need any special training, and if you are a web developer then you'll already feel right at home.

For this guide we'll create a blog and explain what we do step by step. A blog is just a listing of posts/articles as well as some pages. Posts are like status updates on how something is going. Pages on the other hand are something we always want to show.

Great! Lets get started. Oh, and if you ever get stuck, have a question, or need help - [then jump onto any of our official support channels and we'll be right with you](/support). Cheers!










## Creating the Standard Project Structure

Before we get hacking away on content, we have to create our project and set it up with the [standard structure](/docpad/overview) that DocPad uses. To do this, we'll run the following:

``` bash
mkdir my-website
cd my-website
docpad run
```

When prompted for a skeleton, select `No Skeleton` - that'll set up our standard directory structure for us automatically. The `docpad run` command will also keep running once the action has completed successfully - this is because it also watches for changes and will regenerate our website when changes occur - it'll also start a web server on [http://localhost:9778](http://localhost:9778) so we can view our website as we go.

For now, we'll keep `docpad run` running, but whenever you want to stop it, just hit `CTRL+C` on your keyboard to exit it.


## Adding the Home Page

Lets create our first document, our home page for our website. So lets create the document `src/documents/index.html` and give it the following content:

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

Once you've saved it, if you go to [http://localhost:9778](http://localhost:9778) you'll notice that DocPad has already regenerated your website and you'll see the the page we created above rendered by the browser. Fantastic!











## Adding the About Page and a Layout

Now that's done, we'll want to add our "About Me" page so people browsing our website can know who we are! To do this, lets create a new document at `src/documents/pages/about.html` and give it the content:

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

Now if we go to [http://localhost:9778/pages/about.html](http://localhost:9778/pages/about.html) we'll be able to see that page in our browser! Awesome.

However, duplicating that layout information inside our home page and our about page is pretty redundant. For instance, if we wanted to change the contents of `<head>` to something else, then we'll have to change it in two places! This is where layouts come in.

Layouts wrap around our documents, so we can define the surrounding areas of a document only once! So what we will do is move the wrapper stuff of our two documents into a new layout located at `src/layouts/default.html.eco`. Doing so, we'll end up with the following:

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

- `src/documents/index.html`

	``` erb
	---
	title: "Welcome!"
	layout: "default"
	---

	<p>Welcome to My Website!</p>
	```

- `src/documents/pages/about.html`

	``` erb
	---
	title: "About Me"
	layout: "default"
	---

	<p>I like long walks on the beach. <strong>Plus I rock at DocPad!</strong></p>
	```

However, if you go to either the home page or the about page on our web server, you'll notice that their content is just the layout, and don't actually contain any of the document content! This is because we haven't installed the templating engine for our layout yet!


### Installing the Templating Engine

Templating Engines allow us to embed abstractions inside our documents - which is why we have to use them for layouts, as a layout is an abstraction, an abstraction that wraps around a document and outputs the document's content in a specific way :)

For this guide, the templating engine we'll be using is [eco](https://github.com/sstephenson/eco) and is available to us via the [eco plugin](http://docpad.org/plugin/eco). So lets install that now by quitting DocPad (`CTRL+C`), and running:

``` bash
npm install --save docpad-plugin-eco
```

Once installed, if we run DocPad again (`docpad run`), then go our home page or about page, we'll see that the content actually contains the document content! In other words, it's actually rendered correctly through our eco templating engine! Woot woot.

Now, why did we do use `<%=` for the document's title, but `<%-` for the document's content? The reasoning for this is that `<%=` will escape the data we give it before outputting the data, whereas `<%-` we output it without escaping it. So why should we escape some things, and not escape others? Generally, whenever the data we want to output is HTML (so the document's content) we want to output it "as is" so without any escaping, however if the content isn't HTML then we want to output it having it escaped. The reasoning for this is say the document title is `3 is > 2` then if we were to output it unescaped we could end up with something like `<title>3 is > 2</title>` which is invalid HTML due to the `>`, however if we were to output it escaped, we would get `<title>3 is &gt; 2</title>` which is valid HTML and will look exactly the same to the user :)


### A note on Plugins

Now while we use the eco templating engine in this guide, there are plenty of other templating engines we could use too! We find eco is the most beginner friendly as it is most like HTML, however after experimenting with some of the others you may find you'd like to use them instead. Adding support for a new templating engine is as simple as installing the plugin for it.

But DocPad also supports more than just templating engines, we have a whole range of different plugins to do different things! So be sure to check out everything we've got.

[You can find the full listing of plugins we have on the Plugins Page](/docpad/plugins).


### A note on Rendering

Now the reason we can support multiple templating engines is because of the way DocPad renders things - which is extension by extension - so by doing `src/layouts/default.html.eco` we say render from eco to html due to the order of the extensions. For instance, if we did `default.eco.html` we'd want to render from `html` to `eco` which isn't possible - but for somethings like CoffeeScript to JavaScript, you can also do JavaScript to CoffeeScript given you have the right plugins installed. You can also mix and match extensions by doing something like `default.html.md.eco` which renders from eco to markdown, then markdown to html - allowing you to apply abstractions with eco to your markdown documents! Awesome - but for now, way over our scope! hehe. So lets get back on track.


### A note on Meta Data

Now what on earth was with the stuff between the `---` at the top of our documents! That stuff is our _Meta Data_. It is where we can define extra information about our document, such as its title, layout, date, whatever - you are not limited to what you can define here, it's up to you. However there are some pre-defined properties that serve special purposes (such as layout which we just used).

[You can learn more about meta data and all the special properties on the Meta Data Page.](/docpad/meta-data)


## Adding the Live Reload Plugin and Blocks

### Adding the Live Reload Plugin

Sweet. So we're going good so far. We've got two documents going, and a layout to abstract them. But as we are making this changes, it sure would be nice if our browser refreshed the page automatically. We can do this with the [live reload plugin](http://docpad.org/plugin/livereload), so lets install that now:

``` bash
npm install --save docpad-plugin-livereload
```

Then once you've restarted DocPad, whenever you make a change to the files you'll notice the browser still doesn't refresh automatically to show the changes! Why? The reason is that we have to add our Blocks.

### Adding the Blocks

Blocks are a way for plugins and even ourselves to be able to easily add scripts, styles and meta elements to our pages. In the instance of the live reload plugin, it needs the script block to be able to inject the needed scripts into the page so it can refresh browser whenever changes are made. There are many use cases for blocks, but one thing at a time.

So to add the three default blocks to our layout, we'll update our layout to become:

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

Saving that, and manually reloading our browser, we'll notice that our page now has the needed scripts injected right where the scripts block was outputted. Now if we make a change to any of the files, we'll notice the browser will automatically refresh. Amazing!











## Adding some Template Data and Template Helpers via a Configuration File

### Purpose of a Configuration File

The [DocPad Configuration File](/docpad/config) allows us to configure our DocPad instance, listen to events, and perform some nifty abstractions.

Consider the case where our document title is empty. With our current solution the title of the page would be ` | My Website`, in which case just having `My Website` would be far more ideal when our document doesn't have a title.

We could update our title code in our layout template to become:

``` erb
<title><%= if @document.title then "#{@document.title} | My Website" else "My Website" %></title>
```

Which would achieve the goal, but then we have to update the website title in two places if we want to use something else besides `My Website`, and considering this a common abstraction it would be nice if we could abstract it out, say into a configuration file!

So lets create our configuration at the location `my-website/docpad.coffee` and give it the contents:

``` coffee
# Define the Configuration
docpadConfig = {
	# ...
}

# Export the Configuration
module.exports = docpadConfig
```

The first part is where we actually define our configuration, and the second part is a [node convention](http://nodejs.org/docs/latest/api/modules.html#modules_module_exports) for exporting data from one file to another. Whenever we say add some configuration, you'll want to add it to the `docpadConfig` object we just defined.


### Using TemplateData for Abstractions

Everything that is available to our templates is called [TemplateData](/docpad/template-data) - for instance `@document` is part of our template data. So to be able to abstract out something that our templates wil use, we will need to extend our template data. We can do this by modifying our template data configuration property like so:

``` coffee
docpadConfig = {
	# ...
	templateData:
		site:
			title: "My Website"
	# ...
}
```

With that, our website title is now abstracted out. We can now update our title element in the template to look be:

``` erb
<title><%= if @document.title then "#{@document.title} | #{@site.title}" else @site.title %></title>
```

However, if we really wanted to (and we probably do) we can abstract out that logic into a function inside our template data.


### Abstracting Logic into Template Helpers

When using `.coffee` or `.js` files to define our Configuration File, we are allowed to define functions. Doing so, allows us to use functions within our template data - we call these functions Template Helpers.

When calling a template helper, the scope of the template helper is exactly the same as the scope of what is calling it. This makes abstracting out logic really really easy. Lets see what it would look like:

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

And our template would become:

``` erb
<title><%= @getPreparedTitle() %></title>
```

Now that is awesome. While this was a simple example, we can use this to do some really cool stuff. For instance, [here is an example of it being used to localise dates into french](https://gist.github.com/4166882).

If you're writing a plugin, you can use [the extendTemplateData event](/docpad/events) to extend the template data.











## Adding Assets

Now that we have two documents, a layout, and blocks all done. It's time to start adding some assets. Before proceeding with this section, please have read the [DocPad Overview Page](/docpad/overview) so you know what each of the directories within our website structure are for.


### Images

Lets add our logo to our layout's header. We'll [download the DocPad logo](http://d.pr/i/cfmt+) and place it inside our files directory at `src/files/images/logo.gif` (binary files should always go inside the files directory). Then inside our layout, we'll add the following to get our logo on each page:

``` html
<img src="images/logo.gif" />
```


### Stylesheets

Now lets make all our `h1` headers red, to do this lets add a stylesheet file inside our documents directory at `src/documents/styles/style.css` that contains:

``` css
h1 {
	color: red;
}
```

Then to include it inside our pages, we'll update the styles block inside our layout to:

``` erb
<%- @getBlock("styles").add(["/styles/style.css"]).toHTML() %>
```

Upon saving, we'll notice that our browser will automatically reload, and that our css file will be injected into the layout making our header red!



### Scripts

Now lets add a nifty loading effect using JavaScript and the [jQuery JavaScript Library](http://jquery.com). As always, there's plenty of other JavaScript Libaries you can use, but in this guide we'll go with jQuery.

 To do this, we'll forst [download the jQuery library](http://code.jquery.com/jquery.js) and put it inside our files directory at `src/files/vendor/jquery.js`. The reason we use the file directory for vendor files is that it is extremely unlikely we'll ever want to render any vendor files, so having them all inside our files directory is a good choice for consitency and speed.

 Now that we have jQuery inside our project, we'll add our nifty loading effect by adding a script file at `src/documents/scripts/script.js` and let it contain:

``` javascript
(function(){
	$("body").hide().fadeIn(1000);
})();
```
Now that's done, lets add those files to our scripts block in our layout:

``` erb
<%- @getBlock("scripts").add(["/vendor/jquery.js","/scripts/script.js"]).toHTML() %>
```

Upon saving, we'll notice that our content will fade in over a duration of two seconds. Nifty!











## Getting the benefits of Pre-Processors
Pre-Processors are amazing things. They allow us to write documents in one language (the source language), but export them to a different language (the target language). This is extremely benefifical as you always get to use the syntax that you enjoy, instead of the syntax that you are forced to work with - but most importantly, pre-processors usually offer you more robust and clean functionality than the target language supports out of the box, allowing you to make use of modern developers while still working with old languages.


### Using Markdown, a HTML Pre-Processor
Open the About Page we created earlier (`documents/pages/about.html`). HTML's verbose syntax is terrible for writing content that is more text than markup (e.g. articles, comments, etc). Fortunately, [Markdown](http://daringfireball.net/projects/markdown/) ([one of the many HTML Pre-Processors available to us](/docpad/plugins)) is to the rescue!

With Markdown, we can update our About Page's content to become:

``` markdown
I like long walks on the beach. **Plus I rock at DocPad!**
```

Which gives us the same result, but with all the benefits of Markdown. Now, just like all rendering engines, we have to:

1. Indicate the rendering we want to perform - so rename `about.html` to `about.html.md` to indicate we want to render from Markdown to HTML
1. Install the plugin that can do the rendering - so to install the [RobotSkirt Markdown Plugin](http://docpad.org/plugin/robotskirt) we'll run `npm install --save docpad-plugin-robotskirt`

Sweet, you're now ready to rock the house with Markdown.


### Using Stylus, a CSS Pre-Processor
Open the Stylesheet document we created earlier (`documents/styles/style.css`). CSS really hasn't come that far over the years, it has absolutely no abstractions available to us, making it incredibly redundant and painful to write. Fortunately, [Stylus](http://learnboost.github.com/stylus/) ([one of the many CSS Pre-Processors available to us](/docpad/plugins)) is to the rescue!

Using Stylus, we can update our stylesheet's content to become:

``` stylus
h1
	color: red
```

Which gives us the same result, but with all the benefits of Stylus. Now, just like all rendering engines, we have to:

1. Indicate the rendering we want to perform - so rename `style.css` to `style.css.styl` to indicate we want to render from Stylus to CSS
1. Install the plugin that can do the rendering - so to install the [Stylus Plugin](http://docpad.org/plugin/stylus) we'll run `npm install --save docpad-plugin-stylus`

Sweet, you're now ready to rock the house with Stylus.


### Using CoffeeScript, a JavaScript Pre-Processor
Open the JavaScript document we created earlier (`documents/scripts/script.js`). Sometimes people can get a quite annoyed with JavaScript's verboseness, and very annoyed when they forget a comma somewhere and their entire app breaks. Fortunately, [CoffeeScript](http://coffeescript.org/) ([one of the many JavaScript Pre-Processors available to us](/docpad/plugins)) is to the rescue!

Using CoffeeScript, we can update our script's content to become:

``` coffeescript
$("body").hide().fadeIn(1000)
```

Which gives us the same result, but with all the benefits of CoffeeScript. Now, just like all rendering engines, we have to:

1. Indicate the rendering we want to perform - so rename `script.js` to `script.css.coffee` to indicate we want to render from CoffeeScript to JavaScript
1. Install the plugin that can do the rendering - so to install the [CoffeeSCript Plugin](http://docpad.org/plugin/coffeescript) we'll run `npm install --save docpad-plugin-coffeescript`

Sweet, you're now ready to rock the house with CoffeeScript.











## Adding a Menu Listing for our Pages

Remeber our About Page, wouldn't it be nice that when we list more pages, our menu updates automaticaly. It sure would be, so lets do that.


### Updating our Layout

Open up your Default Layout (`src/layouts/default.html.eco`) and before the `h1` we'll add the following:

``` erb
<nav>
	<% for page in @getCollection("html").findAll({relativeOutDirPath:$in:["","pages"]}).toJSON(): %>
		<li>
			<a href="<%= @document.url %>">
				<%= @document.title %>
			</a>
		</li>
	<% end %>
</nav>
```

Save it, and bang, now we've got our navigation menu on each page! Wicked. So what does that do? Well first it uses the `getCollection` [template helper](/docpad/template-data) to fetch the `html` collection which is a pre-defined collection by DocPad that contains all the HTML documents in our website. Then with that collection we find all the files that their `relativeOutDirPath` [attribute](/docpad/meta-data) set to either `''` (so empty - like our `index.html` file) or `'pages'` (like our About Page). With that we then convert it from a [Backbone](http://backbonejs.org/#Collection)/[QueryEngine](/queryengine/guide) Collection into a standard JavaScript Array using [`toJSON`](http://backbonejs.org/#Collection-toJSON).

That's a bit of a mouthful, but give it a while and you'll be a pro in no time. There is one major ineffeciency with the above approach, can you guess it?

The ineffeciency is that we perform that query every single time we render a layout, which is a bit silly as the results of that query don't change between renders, so really we only have to query it once and provide access to the results to our collection. Good thing we can do this.


### Creating Custom Collections via the Configuration File

So then, lets go back to our [DocPad Configuration File](/docpad/config) (`docpad.coffee`) and open it up. This time we want to add the following:

``` coffee
docpadConfig = {
	# ...
	collections:
		pages: (database) ->
			database.findAllLive({relativeOutDirPath:$in:["","pages"]})
	# ...
}
```

Then inside our Default Layout, we'll update the `getCollection` line to become:
	
``` erb
<% for page in @getCollection("pages").toJSON(): %>
```

Much better, and way more effecient. Did you spot the difference with the call we used? When creating our custom collections, we use the `findAllLive` call instead of the `findAll` call. The reasoning behind this is that `findAllLive` utilises [QueryEngine's Live Collections](/queryengine/guide) which means that we define our criteria once, then throughout time, we keep our collection up to date. In more technical detail, this works by creating a live child collection of the database collection, the child collection then subscribes to `add`, `remove`, and `change` events of the parent collection (the database collection) and tests the model that the event was for against our child collection's criteria (the pages collection) if it passes the collection it adds it, if it doesn't pass it removes it. This is way way better than querying everything every single time.

So then, what about sorting? That's easy enough, we can sort by changing `database.findAllLive({relativeOutDirPath:$in:['','pages']})` to add a second argument which is the sorting argument `database.findAllLive({relativeOutDirPath:$in:['','pages']},[filename:1])` which in this case will sort by the filename in ascending order. To do descending order we would change the `1` to become `-1`. Now we can sort by any attribute available on our models, which means that we could even add a `order` attribute to our document meta data and then sort by that if we wanted to. There is also a third parameter for paging, to learn about that one as well as what type of queryies are available to you, you can refer to the [QueryEngine Guide](/queryengine/guide)


### Setting Default Meta Data Attributes for our Pages

Considering we'd probably like all our pages to use the default layout, we may be lazy enough to want to set this by default for all our pages without us always having to add `layout: default` to our [meta data](/docpad/meta-data) for each page. Just like everything, its pretty darn easy if you know how, and here's how:

``` coffee
docpadConfig = {
	# ...
	collections:
		pages: (database) ->
			database.findAllLive({relativeOutDirPath:$in:["","pages"]}).on "add", (model) ->
				model.setMetaDefaults({layout:"page"})
	# ...
}
```

So what does this do? Its exactly the same as before, but we use the `add` event automaticaly fired by [backbone](http://backbonejs.org/#Collection-add) whenever a model (a page, file, document, whatever) is added to our collection. Then inside our event, we say we want to set our default meta data attributes for the model - them being setting the layout to `page`.

This ability is priceless when doing more complicated things with DocPad, for instance we use it for this documentation to be able to base the navigation structure of our documentation files off their physical location of our file system pretty easily. For instance, if we have a file `docs/docpad/01-start/04-begin.html.md` we can detect that the project is `docpad` so assign `project: "docpad"` to the meta data, as well as the section is "start" and it is order first - so set `category: "start"` and `categoryOrder: 1` as well, and that our file is `begin` and ordered 4th. That's just one example of more nifty things, there's plenty more you'll discover and event on your own epic journey :)


## Adding the Blog Posts

Finally, adding the blog posts can be left up to an exercise for you to figure out!

- If you need pointers: you'll create a new layout called `post` that will use the `default` layout. From there, you'll create a new directory called `posts` that contains your blog posts. We recommend giving them `date` meta data in the format of `2012-12-25` so you can sort your blog posts by the date in descending order.

- If you get stuck: ust hop on our IRC Support Channel - details available via our [Official Support Channels](/support) listing.











## Deployment

[Deployment is the next page in this guide.](/docpad/deploy)
