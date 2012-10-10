# Beginner Guide
Welcome to the Beginner Guide to DocPad.


## Intro

### Use case
You want to create a website with static and dynamic pages. After you launch the website you plan to regularly add some content, but don't want to bother again about your HTML, code but write the content and be done. Think of blog post in a blog-like website, new creations in an artist portfolio or news articles in a news site.

DocPad allows to write the structure once in a simple manner and then focus on your content.

For this guide, let's imagine we're creating John Doe's website where he talks about animals, which consists of an index page with the last articles, a static "About me" page and articles about animals.


### Requirements
All you need to follow this guide is :

- some knowledge about web development, but no need to be a ninja
- your favorite text editor / IDE
- a computer with an Internet connexion :)


### A few words before we start
DocPad doesn't enforce anything in the resulting website itself. You just have to work from a `src` directory, and DocPad will generate the website in a `out` folder.

This guide is not meant to be exhaustive about DocPad's features. This is a progressive step-by-step guide, that will give you best practices about using DocPad. To learn more about DocPad's features and capabilities, don't hesitate to visit [the Wiki](https://github.com/bevry/docpad/wiki).

Ready ? Let's go !


## Step 1 : Installation
DocPad is very easy to install, as well as Node.js is.


### Installing Node.js
Refer to the [DocPad's Readme](https://github.com/bevry/docpad#readme)


### Installing DocPad
Refer to the [DocPad's Readme](https://github.com/bevry/docpad#readme)

Once you're done with the installation instructions, you're ready to move the next section.


## Step 2 : The layouts
"DocPad is installed, what's next?". Good question. The first step we'll go through is creating a _layout_ for John Doe's website. Think of a layout as a template that wraps around our page's content. Layouts can also wrap around other layouts too.


### Understanding the `src/layouts` folder
All _layouts_ are created in the `src/layouts` folder. They follow a simple naming convention: `[layout-name].html.eco`. "What's `.eco`?". It's the [eco templating engine](https://github.com/sstephenson/eco). Eco allows us to embed CoffeeScript within our templates, by wrapping our CoffeeScript code like this `<% coffeescript code %>`, you can output a variable like `<%= variableName %>`, or output a variable without escaping it using `<%- variableName %>`

> It's important to notehere that while this example uses the `.eco` extension to render our layout with eco, DocPad can also use several other templating engines as well - [you can read more about the renderers available here](https://github.com/bevry/docpad/wiki/Plugins)). Though, for the purpose of this guide we will eco as it is very beginner friendly.


### Creating a default layout
Create a `default.html.eco` file in the `src/layouts` directory, and paste in this small code:

``` html
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <title><%= @document.title or "Joe Doe's Site" %></title>
  <link rel="stylesheet" href="/styles/style.css">
</head>
<body>
<a href="/" class="logo">John Doe loves animals</a>
<%- @content %>
<footer>Copyright 2012 John Doe.</footer>
</body>
</html>
```

The eco part, `<%- @content %>` tells DocPad to insert the page's content here, and the `<%= @document.title or "Joe Doe's Site" %>` part outputs our page's title, or if not present outputs `Joe Doe's Site`. All pages that use the `default` layout will be wrapped in this markup. Simple!

Let's move to the next step!


## Step 3 : Adding static assets
You may have noticed that there's a file referenced in the layout we didn't talk about yet: the css file. It's a static asset, meaning that DocPad will not process nor render it. Adding static assets in DocPad is dead simple:


### Understanding the `src/files` folder
Static assets of your website should live inside the `src/files` folder. Any files that you have in `src/files` will be copied to the `out` directory as is. So for instance `src/files/styles/style.css` will be copied to `out/styles/style.css` when we generate our website.

We can use this folder for static assets like css files, javascript code, images, favicons etc.


### Adding the assets
Create a `src/files/styles` folder, and place inside it a custom css file named `style.css`. When we generate our website this will be outputted to `out/styles/style.css`, and as seen earlier we reference it in our layout using `/styles/style.css`

Let's create content now !


## Step 4 : Creating the index.html page
Having a layout and an asset, we're ready to create some content for our website. We're gonna create the home page, i.e. the index page, but for now it will show some static content.

*Important* : DocPad does not require neither a layout nor an asset of any kind to generate a website. You could directly create a content using none of the DocPad's feature, making a simple and independant HTML page and it would work perfectly. The previous steps were only a mean to smoothly introduce some of DocPad's powerful and nice features.


### Understanding the documents folder
Your website content should live in the `documents` folder. This folder is a special folder for DocPad for several reasons, and holds some of the power features of DocPad. For now, we will focus only on the basic and classic usage : adding static content. This static page will display a basic content, and declare the usage of the `default` layout in its metadata (more on this after).

The way _documents_ are copied by DocPad is the same than for assets. The directory structure will be kept intact. This is important because when talking about HTML pages, the directory structure corresponds directly to the final url's.


### Creating a page that uses a layout
Create the `src/documents` folder, and create a `index.html` file. In this file, paste this :

``` html
---
layouts: default
title: "John Doe loves animals"
---

<article>
  <h2>My favorite animal : the cat !</h2>

  <div class="date">written on <span class="date">2012-05-19</span></div>
  <p>Who doesn't love cats ? </p>
</article>
```

You noticed the special content between the `---` delimiters ? The zone delimited is called the _header_ and its content is a document's _metadata_. DocPad can read and make use of any property wrapped between the `---` delimiters and separate them from the rest of the file which will be considered as the document's content.

Here we're asking DocPad to use the `default` layout we created before for this document. When DocPad renders this page, its content will be inserted in place of the `<%- @content %>`. Below is the generated HTML markup.

``` html
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <title>John Doe loves animals</title>
  <link rel="stylesheet" href="/css/styles.css">
</head>
<body>
<a href="/" class="logo">John Doe loves animals</a>
<article>
  <h2>My favorite animal : the cat !</h2>

  <div class="date">written on <span class="date">2012-05-19</span></div>
  <p>Who doesn't love cats ? </p>
</article>
<footer>Copyright 2012 John Doe.</footer>
</body>
</html>
```

We'll talk about metadata and the power they hold, but for now let's generate the first version of our website !

## Step 5 : Using the CLI to generate the website

### The CLI

DocPad is manipulated through the CLI, the Command Line Interface. This is the _Console_ under Linux, the _Terminal_ under Mac OS X, and the _Command.exe_ under Windows. This guide is written under Mac OS X, but the commands are the same under Linux.

DocPad offers several commands to create and render the website. They're documented in the in [Getting Started](https://github.com/bevry/docpad/wiki/Getting-Started) wiki page, under the section "Using the CLI". Here we'll present only the necessary commands to generate the website.

### Generating the website

To render the content under the `src` directory, open your console/terminal and move to your _root_ directory, i.e. the directory that contains the `src` folder. Then type the following commands :

```
npm install docpad-plugin-eco
docpad generate
```

The first command installs the eco renderer plugin, the plugin that handles the `.eco` files like our layout (the `default.html.eco` file). This is needed because by default DocPad comes without any plugin activated, to keep it light and fast. The installation should take only a few seconds, and is needed only once at the beginning. Then every generation will automatically makes use of it when needed.

Then, DocPad will prompt you with a welcome message and will start generating the website. After a few seconds (DocPad is fast !), a new `out` directory will be created with the resulting website, ready to be published.

Then you have 2 choices to view the result :

1. Manually open `out/index.html` in your favorite web browser
2. (Preferred) Use the `docpad server` command to emulate a real web server.

The `docpad server` command will prompt you with a message like this :

`info: DocPad listening to http://localhost:9778/ on directory [root]/out`

where [root] is the _root_ directory of the website. To see your website, simply copy-and-paste the `http://localhost:9778/` url in your web browser. As long as the `docpad server` command is not terminated (using `Ctrl+C` in Linux/Mac), you can visit all of the pages of the website.

You should now see John Doe's wonderful home page ! Awesome.

At this point you should begin to understand how DocPad works in a basic usage and be ready to create your own website with static content. Before leaving you on your own, let's continue by adding some dynamism to the website by using some neat DocPad features.

## Step 6 : Using metadata

### Understanding a document's metadata

Remember the _metadata_ on top the `index.html` file ? _Metadata_ are containers for data that is not part of the content of a document, but can be displayed to create dynamic pages. We already used them to specify the layout of our home page. It would be cool to use metadata like the document's name and its date ? Easy with DocPad ! Let's see how to achieve this.

### Using the metadata

In the `index.html` file, add some metadata in the header like so :

```
---
layout: default
title: "My favorite animal : the cat !"
date: 2012-05-19
---
```

Now let's use them in our document and the layout.

#### Metadata in the document

DocPad allows us to use the document's metadata in the document itself. It's useful to avoid messing with the markup and re-use a metadata multiple times. Here we're going to use its title and date in order to show how to use them.

To use a document's metadata in the document itself, we need to use the Eco template language. In order to do so, we need to rename the file. Rename the `index.html` file to `index.html.eco`, and change its content (not its header) to :

``` html
<article>
  <h2><%= @document.title %></h2>

  <div class="date">written on <span class="date"><%= @document.date.toShortDateString() %></span></div>
  <p>Who doesn't love cats ? </p>
</article>
```

Notice that we replaced the title wrapped in the `h2` tags by `<%= @document.title %>`, and the date by `<%= @document.date.toShortDateString() %>`. We're basically asking DocPad to use its metadata. Regarding the date, if we had written `<%= @document.date %>` the result would have been _Sat May 19 2012 02:00:00 GMT+0200 (CEST)_. It's because DocPad makes use of dates internally, but it offers a few helper functions to display dates in a fancier manner. Using `<%= @document.date.toShortDateString() %>` will display _May 19 2012_,  which is much nicer, right ?


#### Metadata in the layout
Metadata in a layout works the same way than in a document. You have access to the same metadata in the same way, using Eco markup. Here we're going to use the document's title and insert it in the `title` tag of the HTML `head`. So we're adding a dynamic title the index.html page. Cool !

To do this, change the `<title>` line of the `default.html.eco` file to :

``` html
<title><%= @document.title %> - John Doe loves animals</title>
```

With this setup, the title of our current home page will be _My favorite animal : the cat ! - John Doe loves animals_. Easy, isn't it ?


#### A last word about metadata
DocPad offers several metadata like `tags` (an array of tags), `content` (we used it in our layout) or `ignored` (use it to prevent DocPad from rendering a document). A cool feature from DocPad is that you're completely free to add your own custom metadata, with the names and values of your choice ! Those custom metadata work exactly the same way than existing ones, so no limitation here.


## Step 7 : Nested layouts
As we saw it's easy to write static document in DocPad, using regular HTML for the content a few Eco tags when needed. Now we're going to add the various articles about animals.

In John Doe's website, every article will be presented the same way : the title in the same HTML tag, the content inside a `p` tag etc. This is the case for most websites, where content of the same "type" have the same layout. Would it be cool to write the content in plain text, specify its layout once and let DocPad generate the proper markup for us ? It's easy with DocPad, thanks to nested layouts !

Let's see how to do that.


### Understanding nested layouts
We already saw how to create a layout for a document. The cool thing is that we can add the `layout` metadata in a layout file itself, so this layout is embedded in another layout.

Let's create such a layout for John Doe's articles.


### Creating a dynamic page
This is a 2 steps process. First, we're going to add a new layout. Then write our document as plain text and let DocPad do its magic for us.

Step 1 - Create a new `article.html.eco` file in the `src/layouts` folder, and paste this content :

``` html
---
layout: default
---

<article>
  <h2><%= @document.title %></h2>

  <div class="date">written on <span class="date"><%= @document.date.toShortDateString() %></span></div>
  <%- @content %>
</article>
```

It's a classic layout file, like `default.html.eco`, with metadata added in a header. Layouts can have metadata, and even custom ones ! Here we're telling DocPad to wrap the content of this layout in the `default` layout, so that articles appear in a complete HTML page.

Step 2 - Let's add an article. Create a `dogs-are-wonderful-too.html.md` file in `src/documents`, like this :

```
---
layout: article
title: "Dogs are wonderful, too !"
date: '2012-05-20'
---

You know that dogs are man's best friend ? It's because they love us when we love them !
```

The new thing here is the `.md` extension at the end of the file. It stands for [Markdown](http://daringfireball.net/projects/markdown/syntax), a simple language that removes all kind of markups from a text to emphasize readability. To quote from the original project :

```
Readability, however, is emphasized above all else. A Markdown-formatted document should be publishable as-is, as plain text, without looking like it’s been marked up with tags or formatting instructions.
```

DocPad uses [GitHub Flavored Markdown](http://github.github.com/github-flavored-markdown/), that adds some enhancements to the original Markdown. Feel free to read this page to understand the small differences. All wiki pages in GitHub, including this very page, can be written using GitHub Flavored Markdow (and this page is).

Back to John Doe's website. As for Eco, the Markdown renderer is a plugin. Installing it is as easy as typing this command in your console/Terminal :

`npm install docpad-plugin-markdown`

DocPad will then be able to transform any document ending with `.html.md` into a plain HTML page. Here it will embed it into the `article` layout described in the `article.html.eco` file, then embed it into the `default` layout.

You may have noticed that we removed the `<p>` tag around `<%- @content %>` in the `article` layout. This is because GitHub's Markdown automatically wraps a paragraph in a `<p>` tag.

How to see our article page ? As before, head in your console/Terminal, and type :

```
docpad generate
docpad server
```

Then, instead of visiting `http://localhost:9778/`, visit `http://localhost:9778/dogs-are-wonderful-too.html`. Why ? Remember, the path of a document under the `src/documents` file is its url when viewed on the web. As we added the file directly under `src/documents`, we just have to add its name in the url. Had we added it under a new `src/documents/articles` folder, the url would have been `http://localhost:9778/articles/dogs-are-wonderful-too.html`.

The page you should see corresponds to the our content file, wrapped inside the various layouts with metadata calls displayed where asked. John Doe can now create as many articles as he wants about his beloved animals, writing them in plain text using the cool Markdown language, and DocPad will handle the rest. Cool !

### A last word about Eco

A Last thing before we move to the next step of this guide. You have noticed that some the metadata are enclosed in `<%= %>` eco tag, whereas others are inside `<%- %>`. The difference (`-` or `=`) is that Eco _escapes_ the content when using the `=` variation, and displays it as is when using the `-` variation. A good rule of thumb as to when using one or the other : when displaying a document's metadata, use `<%= @document.mymetadata %>` ; when displaying the main content of a document, use `<%- @content %>`.



## Step 8 : Content listing
You now know how to create dynamic pages using layouts and metadata. We will now show you how to create content listings.

John Doe wants to display the five latest articles in his home page, with links to the corresponding pages. To do so and a little more, we'll introduce 2 awesome features of DocPad : the `docpad.cson` file and QueryEngine. Those 2 features requires a better knowledge of Javascript and CoffeeScript, but don't worry, you don't need to be a javascript ninja to understand the usage we're gonna make of them.
Read on !


### The docpad.cson
DocPad allows us to describe some data about our website in a single configuration file, the `docpad.cson` file. This file should be located in the root folder of the website, at the same level of the `src` and `out` folders. The `.cson` extension comes from the [CSON](https://github.com/bevry/cson) library. It allows to write `.json` files in CoffeeScript, and DocPad uses it for this file.

We're going to show basic usage of the file. A good practice is to store in this file the textual elements common to all or several pages of the website. The website name and author are good examples, as well as a common footer message. To add such data, create a `docpad.cson` file in the root folder, and paste the content below. The content is easy to understand and is self-documented, read the comments to understand it :

```
# The DocPad Configuration File
# It is simply a CoffeeScript Object that is parsed by CSON
# The lines starting with a '#' are comments
{
  # TemplateData data are accessible directly from the 'this/@' keyword in layouts and documents.
  templateData:
    # Let's create a place where we gather all data about the site...
    site:
      # ... like its author ...
      author: "John Doe"
      # ... its name ...
      name: "John Doe loves animals"
      # ... and a custom footer message. The """ notation comes from CoffeeScript and is used to embed long strings and can contain HTML tags too.
      footerMessage: """
        John Doe loves animals is property of John Doe. Copyright 2012 John Doe. All your animals are belong to us.
      """
}
```

With such a file, we could display the site name in an Eco file by writing `<%= @site.name %>`. Easy, right ? The important thing here is that under `templateData` no naming convention is enforced, you're free to name and organize your custom data as you see fit.

Let's add them in `default.html.eco`, like this :

``` html
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="author" content="<%= @site.author %>" />
  <title><%= @document.title %> - <%= @site.name %></title>
  <link rel="stylesheet" href="/css/styles.css">
</head>
<body>
<a href="/" class="logo">John Doe loves animals</a>
<%- @content %>
<footer><%= @site.footerMessage %></footer>
</body>
</html>
```

The `docpad.cson` possibilities are beyond the scope of this guide. To discover them, I suggest looking at the well documented example [`docpad.cson`](https://github.com/bevry/website.docpad/blob/master/docpad.cson) file from the [website.docpad](https://github.com/bevry/website.docpad) skeleton.

### QueryEngine

DocPad, in its internals, creates a "database" of all the content located in the `src` folder and gives access to it through [QueryEngine](https://github.com/bevry/query-engine). QueryEngine provides extensive Querying, Filtering, and Searching abilities for [Backbone.js](http://documentcloud.github.com/backbone/) Collections as well as JavaScript arrays and objects. For the technical note, every content in DocPad's internals is represented as a Backbone Model. (I can see some of you smiling :)

DocPad provides a few Collections ready to use :

 - `database` is a Collections of all files under the `src` folder
 - `documents` is a collection of all files under the `src/documents` folder
 - `layouts` is a collection of all files under the `src/layouts` folder
 - `files` is a collection of all files under the `src/public` folder

What that means is that we can use QueryEngine to select very precisely some pieces of content from the `documents` collection, and display them where we want in our website.

We could directly use QueryEngine capabilities in our home page file, writing a complete query directly in our template. But instead, we will declare the collections we want to use in the docpad.cson file and make use of it in our template.

The `docpad.cson` file gives us the possibility to describe custom collections using the QueryEngine API. Just add a `collections` entry and start describing the collection :

``` coffee
# The DocPad Configuration File
# It is simply a CoffeeScript Object which is parsed by CSON
{
  # We're extending the core collections object
  collections:
    # This collection named 'articles' fetches the documents with the 'layout' property set to 'article'
    articles: (database) ->
      database.findAllLive({layout: 'article.html.eco'}, {date:-1})
}
```

Let's break up the code we've added and explain step-by-step.

- `collections:` : We're telling DocPad that we're going to declare custom collections. This line is mandatory and every custom collection must be indented below this line.

- `articles: (database) ->` : We're telling DocPad that our new custom collection is called `articles`. The name could whatever you like, apart from the core collections (`documents`, `layouts`, `files`). The rest of the line is mandatory as well, it means that we're using the whole DocPad's database to create our custom collection.

- `database.findAllLive({layout: 'article.html.eco'}, {date:-1})` : This is where the magic happens. This line of code makes use of the [QueryEngine API](https://github.com/bevry/query-engine/wiki/Using). What we are doing here is find everything from the database with the layout `article.html.eco`, sorting by `date` in descending order (for ascending use `1` instead of `-1`), and always keep it up to date (this is the `Live` bit in `findAllLive`).

That's it ! Our custom collection is ready, and whenever we'll make use of it it will always be up-to-date.

QueryEngine is way more powerful than that, but it's beyond the scope of this guide. Visit [API Guide](https://github.com/bevry/query-engine/wiki/Using) to learn more about it.

### Creating a dynamic homepage

Now we have everything in place to display a list of articles and to create a dynamic homepage.

First create others articles the same way we created `dogs-are-wonderful-too.html.md` and `my-favorite-animal-the-cat.html.md`.

When you're done, we're going to change our static `index.html` home page and transform it into a dynamic page.

Let's rename `index.html` to `index.html.eco`. Now we can write Eco code to make use of our custom collection.

In `index.html.eco`, add a title metadata which value is the title of our home page :

```
---
layout: default
title: John Doe loves animals
---
```

Then change its content to :

``` eco
<ul>
<% for article in @getCollection('articles').toJSON()[0..4] : %>
  <li>
    <h3><%= article.title %></h3>
    <div class="date">written on <span class="date"><%= article.date.toShortDateString() %></span></div>
    <a href="<%= article.url %>">Read the full article</a>
  </li>
<% end %>
</ul>
```

Again, let's explain this code step by step :

#### Step 1 : Looping through our custom collection.

```
<% for article in @getCollection('articles').toJSON()[0..4] : %>
  ...
<% end %>
```

We're looping in each article of our custom `articles` collection. The important things here :
 1. We're using the `for ... in ...` loop from CoffeeScript, that allows us to loop through each element of an array (an array is a list of elements).
 2. The `article` word is deliberately choosen, you could use any word you like.
 3. `@getCollection('articles')` is a helper function provided by DocPad to retrieve a collection. Pass it the name of any collection, core or custom.
 4. `.toJSON()` is a helper provided by Backbone to transform a Backbone.Collection object to an array. We call it to so the `for` loop can work.
 5. `[0..4]` comes from CoffeeScript and allows to limit the number of elements in an array to 5. We just converted the Collection into an Array with `toJSON()`, so it works fine to limit results here. If you're wondering why we go up to 4 and not 5, it's because computers start to count from 0... So "from 0 to 4" really means "from the first to the fifth" !
 5. The `:` at the end of the `for` line and the `<% end %>` come from Eco. They delimit what will happen inside the loop.

#### Step 2 : Printing each collection element.

Inside the loop, everything written will appear in the final markup for each element of our collection. Here's we're just printing a list of article's title, along with its date and a link to the full article.

Some explanations :

- `<%= article.title %>` will print the `title` as we wrote it in our articles' metadata
- `<%= article.date.toShortDateString() %>` : If we had printed `article.date` directly, it would have printed something like `Sun May 20 2012 02:00:00 GMT+0200 (CEST)`, which is not very user-friendly. Hopefully DocPad provides the `toShortDateString()` helper function to format the date in a much nicer way.
- `<%= article.url %>` is using the `url` metadata, set by DocPad and automatically containing the path to the document.

And we're done ! We can now `docpad generate` then `docpad server` our site and view the result in our web browser of choice, where we'll see a home page with a header and a footer and in-between the list we just created, and the links work too. Pretty cool !

## A last word

To sum it up :

1. We create a global layout (`default.html.eco`), and a document specific layout `article.html.eco`.
2. We created some content.
3. We added some site-wide data in `docpad.cson`, as well as a custom collection of articles.
4. We used these site-wide data in our global layout, and the custom collection in our home page to create a dynamic listing of content.

This is all it takes to start making use of the power hidden under DocPad. The way presented above is by no mean the _right way_, as there's no such thing in DocPad. But dividing pages into layout and content, and using the `docpad.cson` file for site-wide data and collections is a best practice I recommend that's all about _separation of concern_, a good habit in programming in general.

We've just skimmed the surface of DocPad, but what we saw should already give you enough power to create your own website. Feel free to ask questions in the [issue tracker](https://github.com/bevry/docpad/issues), and even edit this guide !