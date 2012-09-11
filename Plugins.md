Here is a listing of all the plugins available for DocPad. If you have created a plugin, be sure to list it here :-)

## Installing

To install a plugin, do a `npm install -f docpad-plugin-#{pluginName}` inside your website's directory. For instance, to install the [eco](https://github.com/bevry/docpad-extras/tree/master/plugins/eco/) plugin, you would do `npm install -f docpad-plugin-eco`


## Renderers

These plugins add support for extra markups and languages to DocPad

- [coffeescript](https://github.com/bevry/docpad-extras/tree/master/plugins/coffeescript/) - Supports [CoffeeScript](http://jashkenas.github.com/coffee-script/) to JavaScript `.js.coffee`
- [coffeekup](https://github.com/bevry/docpad-extras/tree/master/plugins/coffeekup/) - Supports [CoffeeKup](http://coffeekup.org/) to anything `.anything.coffee`
- [eco](https://github.com/bevry/docpad-extras/tree/master/plugins/eco/) - Supports [Eco](https://github.com/sstephenson/eco) to anything `.anything.eco`
- [haml](https://github.com/bevry/docpad-extras/tree/master/plugins/haml/) - Supports [HAML](http://haml-lang.com/) to anything `.anything.haml`
- [handlebars](https://github.com/bevry/docpad-extras/tree/master/plugins/handlebars/) - Supports [Handlebars/Moustache](http://handlebarsjs.com/) to anything `.anything.hb|hbs|handlebars`
- [hogan](https://github.com/bevry/docpad-extras/tree/master/plugins/hogan/) - Supports [Hogan/Mustache](http://twitter.github.com/hogan.js/) to anything `.anything.hogan`
- [html2coffee](https://github.com/bevry/docpad-extras/tree/master/plugins/html2coffee/) - Supports HTML to CoffeeKup `.coffee.html`
- [html2jade](https://github.com/bevry/docpad-extras/tree/master/plugins/html2jade) - Supports HTML to [Jade](http://jade-lang.com/) `.jade.html`
- [jade](https://github.com/bevry/docpad-extras/tree/master/plugins/jade/) - Supports [Jade](http://jade-lang.com/) to anything `.anything.jade`
- [js2coffee](https://github.com/bevry/docpad-extras/tree/master/plugins/js2coffee/) - Supports JavaScript to CoffeeScript `.coffee.js`
- [less](https://github.com/bevry/docpad-extras/tree/master/plugins/less/) - Supports [LessCSS](http://lesscss.org/) to CSS `.css.less`
- [marked](https://github.com/bevry/docpad-extras/tree/master/plugins/marked/) - Supports [Markdown](ttp://daringfireball.net/projects/markdown/basics) to HTML `.html.md|markdown`
- [move](https://github.com/bevry/docpad-extras/tree/master/plugins/move) - Supports [Move](http://movelang.org/) to JavaScript `.js.move`
- [php](https://github.com/bevry/docpad-extras/tree/master/plugins/php) - Supports [PHP](http://php.net/) to anything `.anything.php|phtml`
- [ruby](https://github.com/bevry/docpad-extras/tree/master/plugins/ruby) - Supports [Ruby](http://www.ruby-lang.org/) and [ERuby](http://en.wikipedia.org/wiki/ERuby) to anything `.anything.ruby|erb`
- [sass](https://github.com/bevry/docpad-extras/tree/master/plugins/sass/) - Supports [SCSS and SASS](http://sass-lang.com/) to CSS (includes [compass](http://compass-style.org/) support) `.css.sass|scss`
- [stylus](https://github.com/bevry/docpad-extras/tree/master/plugins/stylus/) - Supports [Stylus](http://learnboost.github.com/stylus/) to CSS `.css.styl|stylus`


## Helpers

These plugins add extra functionality to DocPad

- [associatedfiles](https://github.com/bevry/docpad-extras/tree/master/plugins/associatedfiles) - Lets you easily associate files to a particular document, and then grab the collection for them
- [buildr](https://github.com/bevry/docpad-extras/tree/master/plugins/buildr/) - Supports bundling scripts and styles (including pre-processors like coffeescript, less, etc) using [Buildr](https://github.com/balupton/buildr.npm)
- [cachr](https://github.com/bevry/docpad-extras/tree/master/plugins/cachr/) - Allows you to cache remote urls locally from within your templates
- [cleanurls](https://github.com/bevry/docpad-extras/tree/master/plugins/cleanurls/) - Adds support for urls like `/blog/hello` as well as the original url `/blog/hello.html`
- [feedr](https://github.com/bevry/docpad-extras/tree/master/plugins/feedr/) - Allows you to render remote feeds within your templates
- [highlightjs](https://github.com/chase/docpad-plugin-highlightjs) - Adds [Highlight.js](https://github.com/isagalaev/highlight.js) syntax highlighting to code snippets
- [livereload](https://github.com/bevry/docpad-extras/tree/master/plugins/livereload) - Automatically reloads the page whenever a regeneration is performed
- [partials](https://github.com/bevry/docpad-extras/tree/master/plugins/partials/) - Adds the ability to create re-usable partials for your templates within DocPad
- [pygments](https://github.com/bevry/docpad-extras/tree/master/plugins/pygments/) - Adds [Pygments](http://pygments.org/) syntax highlighting to code snippets
- [related](https://github.com/bevry/docpad-extras/tree/master/plugins/related/) - Scans your documents `tags: 'tag1', 'tag2'` metadata to produce a listing of related documents
- [text](https://github.com/bevry/docpad-extras/tree/master/plugins/text/) - Render templateData properties without needing template engine, useful for abstraction in configuration files


## Older plugins

These plugins are for older versions of DocPad, or have been deprecated in favour of other plugins.

- [markdownreferencelinks](https://github.com/Delapouite/docpad-markdownreferencelinks) - Provides a way to put links references into the header of a document so they can be used later inside its markdown content
- [markdown](https://github.com/bevry/docpad-extras/tree/master/plugins-old/markdown/) - Supports [Markdown](ttp://daringfireball.net/projects/markdown/basics) to HTML `.html.md|markdown` - deprecated in favor of marked


## Requested

[Here is a list of plugins waiting to be coded up :-)](https://github.com/bevry/docpad/issues?labels=plugin&sort=created&direction=desc&state=open&page=1)