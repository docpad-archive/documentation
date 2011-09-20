### What is a document's meta data?

At the start of each document is an optional area right up the top that looks something like this

    ---
    title: "My awesome blog post"
    ---

That is your document's meta data. It won't be included in the output of the document, as is where you can assign extra data to your document such as title, date, tags, etc.


### Is a document aware of it's meta data?

It sure is, if you are using eco as the rendering engine, you can totally do this:

    ---
    title: "My awesome blog post"
    meaningOfLife: 42
    ---

    What is the meaning of life? <%= @document.meaningOfLife %>

To use eco, simply ensure that you have the extension `.eco` at the end of your file. E.g. `my-blog-post.html.eco`. It doesn't have to be at the end, but it mustn't be the first extension.


### What do the extensions mean?

The extensions `.html.eco` means process this with Eco and render it as HTML. Alternatively, we can get pretty inventive and do something like this: `.html.md.eco` which means process this with Eco, then Markdown and finally render it as HTML.


### How do I hide a document from being rendered? E.g. a draft post.

Add the following to your document's meta data

    ignored: true


### I upgraded, and it doesn't work

[Check out the Upgrade Guides here](https://github.com/balupton/docpad/wiki/Upgrading)