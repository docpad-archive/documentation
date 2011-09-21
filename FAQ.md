### What is a document's meta data?

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


### Help! Whenever I output a variable (like `content`) it is escaped (`<` rendered as `&lt;`)?

Template engines by default _escape_ all variable output. Escaping is when we turn things like the open bracket `<` into it's _html entity_ equivalent `&lt;`. This helps prevent malicious code accidentally being injected into your website which can open the door to XSS attacks. As such, we have to use a special syntax to keep the variable _unescaped_ when outputted. The special syntax is different for the templating engine your using, so here are the ways we know:

- Eco: `<%- content %>` instead of `<%= content %>`
- Jade: `!{content}` instead of `#{content}`
- HAML: `!= content` instead of `= content`


### The growl notifications aren't displaying?

I got confused by this too, turns out you need to download the growl installer from the [growl website](http://growl.info/), and inside it will be another installer at `Extras/growlnotify/growlnotify.pkg` which you need to install too. What this package does it provides command line applications that ability to call growl which is needed as docpad is a command line application.


### I upgraded, and it doesn't work

[Check out the Upgrade Guides here](https://github.com/balupton/docpad/wiki/Upgrading)


### Where can I host my docpad website?

[Check out the Hosting Guide here](https://github.com/balupton/docpad/wiki/Hosting)


### Where can I find tutorials about DocPad?

[Check out the Tutorials Page here](https://github.com/balupton/docpad/wiki/Tutorials)
