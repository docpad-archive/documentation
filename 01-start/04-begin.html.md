```
title: "Beginner Guide"
cssClasses: []
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

So to add the three default blocks to our layout, we'll update our layout to contain:

``` erb
<html>
<head>
	<title><%= @document.title %> | My Website</title>
	<%- @getBlock("meta").toHTML() %>
	<%- @getBlock("styles").toHTML() %>
</head>
<body>
	<%- @content %>
	<%- @getBlock("scripts").toHTML() %>
</body>
</html>
```

Saving that, and manually reloading our browser, we'll notice that our page now has the needed scripts injected right where the scripts block was outputted. Now if we make a change to any of the files, we'll notice the browser will automatically refresh. Amazing!



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
$ ->
	$("body").hide().fadeIn(2000)
```

Which gives us the same result, but with all the benefits of CoffeeScript. Now, just like all rendering engines, we have to:

1. Indicate the rendering we want to perform - so rename `script.js` to `script.css.coffee` to indicate we want to render from CoffeeScript to JavaScript
1. Install the plugin that can do the rendering - so to install the [CoffeeSCript Plugin](http://docpad.org/plugin/coffeescript) we'll run `npm install --save docpad-plugin-coffeescript`

Sweet, you're now ready to rock the house with CoffeeScript.



## Adding the Blog Posts

### Writing the Blog Posts

It's now time for us to add some blog posts. So lets create a new document at 

### Using Markdown


## Listing the Blog Posts

### Creating the Listing for our Home Page

### Displaying the Listing on our Home Page


## Applying Abstractions with a Configuration File

### Adding the Configuration File

It's now time to add our [configuration file](http://localhost:9778/learn/docpad-config). Configuration files can take a few different formats, in this guide we will use the `docpad.coffee` format.

### Applying Template Data Abstractions



## Adding the Assets

Now that we have two documents, a layout, and blocks all done. It's time to start adding assets to our website.


### Stylesheets + Pre-Processors

Lets start by adding a stylesheet located at `src/documents/styles/style.css` that contains:

``` css
h1 {
	color: red;
}
```

And then update our styles block in our layout to become:

``` erb
<%- @getBlock("styles").add(["/styles/style.css"]).toHTML() %>
```

Upon saving, we'll notice that our browser will automatically reload, our css file will be injected into the layout, and our header will now be red! This is getting cool! It can get even cooler though.

If you've ever done CSS before on a large project, you'll know that it really hasn't come far in the past 10 years and is a painfully verbose to write. Luckily, there are things called pre-processors which allow us to write CSS in a much nicer way, and compile that cleaner way into plain CSS that the browser can understand. Pre-processors are a life saver, and for the most part we'll always want to use one.

In this guide, we'll use [Stylus](http://learnboost.github.com/stylus/) by installing the [stylus plugin](http://docpad.org/plugin/stylus). As always, there's plenty of other options which you can discover on our [Plugins Page](/docpad/plugins). Lets install the stylus plugin by doing:

``` bash
npm install docpad-plugin-stylus
```

Once DocPad is restarted, we now have stylus available to us, but we aren't yet using it yet - know why? It's because we need to update the extension for our stylesheet document to say lets use stylus! So lets do that now.

Lets change it from `style.css` to `style.css.styl` and change the content to the following to make use of the awesomeness that stylus gives us:

``` css
h1
	color: red
```

Save, and then bang, our website will have reloaded in our browser and we'll now have red headers just like before - but with a much nicer, powerful, and lenient syntax. Woot woot.


### Files Directory

So far, we have just used the documents directory, but there is also the files directory. 
There are a few key reasons for this:
1. The document directory renders based on extensions, the files directory performs no rendering. Therefore, anything that does not need to be rendered should go inside the files directory.
2. 
1. As the documents directory performs rendering based on extensions, if we were to have a file called `jquery-1.8.2.js` inside the `documents` directory, then DocPad would output it as `jquery-1.8` as it would believe we wanted to render from `2` to `8` due to the extensions. However placing our `jquery-1.8.2.js` file inside the `files` directory doesn't have this issue, as the files directory is not rendered. Generally, anything you don't want to render should go in the files directory.
2. 



### Scripts + Files Directory + Pre-Processors

Next step, is to add a JavaScript file. We don't really need to add one yet, but we'll do it anyway to showcase how you would do so.

Just like as we did with our stylesheets, lets create a document at `src/documents/scripts/script.js` containing:

``` javascript
$(function(){
	$("body").hide().fadeIn(2000);
});
```

Don't forget to update your scripts block in your layout as well!

``` erb
<%- @getBlock("scripts").add(["/scripts/script.js"]).toHTML() %>
```

Now, notice the mentions of `$` in our javascript code? That is because we are using the [jQuery](http://jquery.com/) JavaScript Library. jQuery lets us do a lot of powerful awesome javascript stuff with barely any code. As always, there's plenty of other JavaScript Libaries you can use, but in this guide we'll go with jQuery.

So that JavaScript file we just added will error on you so far, as we haven't installed jQuery yet on our website. To do so, lets [download jQuery](http://code.jquery.com/jquery.js) and put it here `src/files/vendor/jquery.js` and update our scripts block like so:

``` erb
<%- @getBlock("scripts").add(["/vendor/jquery.js","/scripts/script.js"]).toHTML() %>
```

An important thing to notice, is how we put the jquery library into our files directory instead of into our documents directory. The reason for this is that we will never ever want to render jquery, nor will we ever want it to contain meta data - the two things that putting it in the documents directory gives us. Therefore, we will just put it in the files directory. Another important difference is that if we were to name the jquery file something like `jquery-1.8.2.js` and had it in the documents directory, then DocPad would render it from `2` to `8` resulting in the file `jquery-1.8` instead of the original file name - however placing such a file inside our files directory, we don't have that issue as there is no rendering happening in the files directory so file names will remain intact.

Awesome. Now that's covered, lets take advantage of a JavaScript pre-processor called [CoffeeScript](http://coffeescript.org/). CoffeeScript gives us a nice syntax for JavaScript, as well as giving us easy abstractions for complex things in JavaScript - it's well worth reading up about. To update our script file to use CoffeeScript we would install the [CoffeeScript Plugin](http://docpad.org/plugin/coffeescript) by doing:

``` bash
npm install --save docpad-plugin-coffeescript
```

And as always, restart DocPad after any plugin installations. Then rename our script document to use the CoffeeScript extension by changing it from `script.js` to `script.js.coffee` and update its contents to:

``` coffee
$ ->
	$("body").hide().fadeIn(2000)
````


### Awesome


## CONTENTS

- Creating the Standard Directories
- Hello World
	- Create a document
	- Hit redundancy when we want more
- Plugins
	- Install the live reload plugin
	- Quick rundown of plugins
- Adding a stylesheet
	- Create the stylesheet
	- Problems with plain CSS
	- Using Stylus (intro to pre-processors)
- Adding an image
	- Introduction to the files directory
	- Adding the image to files
	- Adding the image to our markup
	- How the directories work together
- Adding a layout
	- Benefits of a layout (in relation to our posts)
	- Create the layout file
	- Take out the layout from our document
	- Introduction to meta data
	- Introduction to eco
- Adding our posts
	- Create the directory
	- Add our posts with layout
	- Make them markdown
- Nested layouts
	- Different layout for the posts
	- How do nested layouts work
- Listing our posts
	- Introduction to collections and models
	- Introduction to querying, sorting
- Further abstractions
	- Configuration files introduction
	- Template data variables
	- Template helpers
	- Collections
- Deployment
	- Generate for static server
	- Different environments
	- Deploy to apache demonstration
- All done
