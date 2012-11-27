Here is a listing of all the plugins available for DocPad. If you have created a plugin, be sure to list it here :-)

## Installing

To install a plugin, do a `npm install --save docpad-plugin-#{pluginName}` inside your website's directory. For instance, to install the [eco](http://docpad.org/plugin/eco/) plugin, you would do `npm install --save docpad-plugin-eco`


## Renderers

These plugins add support for extra markups and languages to DocPad

- [coffeescript](http://docpad.org/plugin/coffeescript/) - Supports [CoffeeScript](http://jashkenas.github.com/coffee-script/) to JavaScript `.js.coffee`
- [coffeekup](http://docpad.org/plugin/coffeekup/) - Supports [CoffeeKup](http://coffeekup.org/) to anything `.anything.coffee`
- [cson](http://docpad.org/plugin/cson/) - Supports [CSON](https://github.com/bevry/cson) to JSON `.json.cson`
- [eco](http://docpad.org/plugin/eco/) - Supports [Eco](https://github.com/sstephenson/eco) to anything `.anything.eco`
- [haml](http://docpad.org/plugin/haml/) - Supports [HAML](http://haml-lang.com/) to anything `.anything.haml`
- [handlebars](http://docpad.org/plugin/handlebars/) - Supports [Handlebars/Moustache](http://handlebarsjs.com/) to anything `.anything.hb|hbs|handlebars`
- [hogan](http://docpad.org/plugin/hogan/) - Supports [Hogan/Mustache](http://twitter.github.com/hogan.js/) to anything `.anything.hogan`
- [html2coffee](http://docpad.org/plugin/html2coffee/) - Supports HTML to CoffeeKup `.coffee.html`
- [html2jade](http://docpad.org/plugin/html2jade) - Supports HTML to [Jade](http://jade-lang.com/) `.jade.html`
- [jade](http://docpad.org/plugin/jade/) - Supports [Jade](http://jade-lang.com/) to anything `.anything.jade`
- [js2coffee](http://docpad.org/plugin/js2coffee/) - Supports JavaScript to CoffeeScript `.coffee.js`
- [less](http://docpad.org/plugin/less/) - Supports [LessCSS](http://lesscss.org/) to CSS `.css.less`
- [marked](http://docpad.org/plugin/marked/) - Supports [Markdown](ttp://daringfireball.net/projects/markdown/basics) to HTML `.html.md|markdown` via [marked](https://github.com/chjj/marked)
- [move](http://docpad.org/plugin/move) - Supports [Move](http://movelang.org/) to JavaScript `.js.move`
- [php](http://docpad.org/plugin/php) - Supports [PHP](http://php.net/) to anything `.anything.php|phtml`
- [ruby](http://docpad.org/plugin/ruby) - Supports [Ruby](http://www.ruby-lang.org/) and [ERuby](http://en.wikipedia.org/wiki/ERuby) to anything `.anything.ruby|erb`
- [robotskirt](http://docpad.org/plugin/robotskirt/) - Supports [Markdown](ttp://daringfireball.net/projects/markdown/basics) to HTML `.html.md|markdown` via [robotskirt](https://github.com/benmills/robotskirt)
- [sass](http://docpad.org/plugin/sass/) - Supports [SCSS and SASS](http://sass-lang.com/) to CSS (includes [compass](http://compass-style.org/) support) `.css.sass|scss`
- [stylus](http://docpad.org/plugin/stylus/) - Supports [Stylus](http://learnboost.github.com/stylus/) to CSS `.css.styl|stylus`


## Helpers

These plugins add extra functionality to DocPad

- [associatedfiles](http://docpad.org/plugin/associatedfiles) - Lets you easily associate files to a particular document, and then grab the collection for them
- [buildr](http://docpad.org/plugin/buildr/) - Supports bundling scripts and styles (including pre-processors like coffeescript, less, etc) using [Buildr](https://github.com/balupton/buildr.npm)
- [cachr](http://docpad.org/plugin/cachr/) - Allows you to cache remote urls locally from within your templates
- [cleanurls](http://docpad.org/plugin/cleanurls/) - Adds support for urls like `/blog/hello` as well as the original url `/blog/hello.html`
- [csv](https://github.com/CycoPH/docpad-plugin-csv/) - Adds support for CSV data mapping. The comma seperated data files work just like a database, map from column 1 to column 2
- [feedr](http://docpad.org/plugin/feedr/) - Allows you to render remote feeds within your templates
- [highlightjs](http://docpad.org/plugin/highlightjs/) - Adds [Highlight.js](https://github.com/isagalaev/highlight.js) syntax highlighting to code snippets
- [livereload](http://docpad.org/plugin/livereload) - Automatically reloads the page whenever a regeneration is performed
- [partials](http://docpad.org/plugin/partials/) - Adds the ability to create re-usable partials for your templates within DocPad
- [pygments](http://docpad.org/plugin/pygments/) - Adds [Pygments](http://pygments.org/) syntax highlighting to code snippets
- [related](http://docpad.org/plugin/related/) - Scans your documents `tags: 'tag1', 'tag2'` metadata to produce a listing of related documents
- [text](http://docpad.org/plugin/text/) - Render templateData properties without needing template engine, useful for abstraction in configuration files


## Older plugins

These plugins are for older versions of DocPad, or have been deprecated in favour of other plugins.

- [markdownreferencelinks](https://github.com/Delapouite/docpad-markdownreferencelinks) - Provides a way to put links references into the header of a document so they can be used later inside its markdown content
- [markdown](http://docpad.org/plugin/markdown/) - Supports [Markdown](ttp://daringfireball.net/projects/markdown/basics) to HTML `.html.md|markdown` - deprecated in favor of marked


## Requested

[Here is a list of plugins waiting to be coded up :-)](http://docpad.org/issues?labels=plugin&sort=created&direction=desc&state=open&page=1)