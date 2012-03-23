It's interesting to see what plugins others have come up with. Link to DocPad plugins here.

## Bundled

These plugins are already bundled with DocPad. [To view all the bundled plugins inside DocPad, click here.](https://github.com/bevry/docpad/blob/master/lib/exchange)

### Renderers

- [Markdown Plugin](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/markdown/markdown.plugin.coffee) - supports [Markdown](ttp://daringfireball.net/projects/markdown/basics) to HTML
- [Coffee Plugin](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/coffee/coffee.plugin.coffee) - supports [CoffeeKup](http://coffeekup.org/) to anything and from HTML, and [CoffeeScript](http://jashkenas.github.com/coffee-script/) to and from JavaScript
- [Eco Plugin](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/eco/eco.plugin.coffee) - supports [Eco](https://github.com/sstephenson/eco) to anything
- [Jade Plugin](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/jade/jade.plugin.coffee) - supports [Jade](http://jade-lang.com/) to anything, and HTML to Jade
- [HAML Plugin](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/haml/haml.plugin.coffee) - supports [HAML](http://haml-lang.com/) to anything
- [Stylus Plugin](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/stylus/stylus.plugin.coffee) - supports [Stylus](http://learnboost.github.com/stylus/) to CSS

### Helpers

- [Buildr Plugin](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/buildr/buildr.plugin.coffee) - Supports bundling scripts and styles (including pre-processors like coffeescript, less, etc) using [Buildr](https://github.com/bevry/buildr.npm)
- [Clean Urls Plugin](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/cleanurls/cleanurls.plugin.coffee) - adds support for urls like `/blog/hello` as well as the original url `/blog/hello.html`
- [Related Pages Plugin](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/related/related.plugin.coffee) - scans your documents `tags: 'tag1', 'tag2'` metadata to produce a listing of related documents. Access them through `@document.relatedDocuments`


## User Created

These plugins you'll have to install manually.

- [Markdown Reference Links](https://github.com/Delapouite/docpad-markdownreferencelinks) - provides a way to put links references into the header of a document so they can be used later inside its markdown content.
- [Images](https://github.com/msutherl/docpad-images) - provide access to an array of paths to images associated with the current document during document rendering


## Waiting to be implemented

[Here is a list of plugins waiting to be coded up :-)](https://github.com/bevry/docpad/issues?labels=plugin&sort=created&direction=desc&state=open&page=1)