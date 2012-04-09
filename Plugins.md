Here is a listing of all the plugins available for DocPad. If you have created a plugin, be sure to list it here :-)

## Bundled

These plugins are already bundled with DocPad

### Renderers

- [Coffee](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/coffee/) - Supports [CoffeeKup](http://coffeekup.org/) to anything and from HTML, and [CoffeeScript](http://jashkenas.github.com/coffee-script/) to and from JavaScript
- [Eco](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/eco/) - Supports [Eco](https://github.com/sstephenson/eco) to anything `.anything.eco`
- [HAML](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/haml/) - Supports [HAML](http://haml-lang.com/) to anything `.anything.haml`
- [Hogan](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/hogan/) - Supports [Hogan/Mustache](http://twitter.github.com/hogan.js/) to anything `.anything.hogan`
- [Jade](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/jade/) - Supports [Jade](http://jade-lang.com/) to anything `.anything.jade`
- [Less](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/less/) - Supports [LessCSS](http://lesscss.org/) to CSS `.css.less`
- [Markdown](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/markdown/) - Supports [Markdown](ttp://daringfireball.net/projects/markdown/basics) to HTML `.html.md|markdown`
- [Stylus](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/stylus/) - Supports [Stylus](http://learnboost.github.com/stylus/) to CSS `.css.styl|stylus`
- [SASS](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/sass/) - Supports [SASS](http://sass-lang.com/) to CSS `.css.sass|scss`

### Helpers

- [Cachr](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/cachr/) - Allows you to cache remote urls locally from within your templates
- [CleanUrls](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/cleanurls/) - Adds support for urls like `/blog/hello` as well as the original url `/blog/hello.html`
- [Feedr](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/feedr/) - Allows you to render remote feeds within your templates
- [Partials](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/partials/) - Adds the ability to create re-usable partials for your templates within DocPad
- [Pygments](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/pygments/) - Adds [Pygments](http://pygments.org/) syntax highlighting to code snippets
- [Related Pages](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/related/) - Scans your documents `tags: 'tag1', 'tag2'` metadata to produce a listing of related documents. Access them through `@document.relatedDocuments`


## Extras

These plugins you'll have to install manually

### Renderers

- [HTML2Jade](https://github.com/bevry/docpad-extras/tree/master/plugins/html2jade) - Supports HTML to [Jade](http://jade-lang.com/)
- [Move](https://github.com/bevry/docpad-extras/tree/master/plugins/move) - Supports [Move](http://movelang.org/) to JavaScript
- [PHP](https://github.com/bevry/docpad-extras/tree/master/plugins/php) - Supports [PHP](http://php.net/) to anything
- [Roy](https://github.com/bevry/docpad-extras/tree/master/plugins/roy) - Supports [Roy](http://roy.brianmckenna.org/) to JavaScript
- [Ruby](https://github.com/bevry/docpad-extras/tree/master/plugins/php) - Supports [Ruby](http://www.ruby-lang.org/) and [ERuby](http://en.wikipedia.org/wiki/ERuby) to anything

### Helpers

- [Buildr Plugin](https://github.com/bevry/docpad-extras/blob/master/plugins/buildr/) - Supports bundling scripts and styles (including pre-processors like coffeescript, less, etc) using [Buildr](https://github.com/bevry/buildr.npm)
- [Markdown Reference Links](https://github.com/Delapouite/docpad-markdownreferencelinks) - Provides a way to put links references into the header of a document so they can be used later inside its markdown content.
- [Images](https://github.com/bevry/docpad-extras/blob/master/plugins/images/) - Provides access to an array of paths to images associated with the current document during document rendering


## Requested

[Here is a list of plugins waiting to be coded up :-)](https://github.com/bevry/docpad/issues?labels=plugin&sort=created&direction=desc&state=open&page=1)