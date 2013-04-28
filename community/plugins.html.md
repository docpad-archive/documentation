Here is a listing of all the plugins available for DocPad. If you have created a plugin, be sure to [include it in this listing!](https://github.com/bevry/docpad-documentation/edit/master/community/plugins.html.md) :)

## Installing

To install a plugin, do a `npm install --save docpad-plugin-#{pluginName}` inside your website's directory. For instance, to install the [eco](http://docpad.org/plugin/eco/) plugin, you would do `npm install --save docpad-plugin-eco`


## Renderers

These are plugins that add support for extra markups and languages to DocPad:

- [coffeescript](http://docpad.org/plugin/coffeescript/) - Supports [CoffeeScript](http://jashkenas.github.com/coffee-script/) to JavaScript `.js.coffee`
- [coffeekup](http://docpad.org/plugin/coffeekup/) - Supports [CoffeeKup](http://coffeekup.org/) to anything `.anything.coffee`
- [cson](http://docpad.org/plugin/cson/) - Supports [CSON](https://github.com/bevry/cson) to JSON `.json.cson`
- [eco](http://docpad.org/plugin/eco/) - Supports [Eco](https://github.com/sstephenson/eco) to anything `.anything.eco`
- [haml](http://docpad.org/plugin/haml/) - Supports [HAML](http://haml-lang.com/) to anything `.anything.haml`
- [hamlcoffee](https://github.com/ashnur/docpad-plugin-hamlcoffee/) - Supports [HAML-COFFEE](https://github.com/netzpirat/haml-coffee/) to HTML `.html.hamlc`
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

These are plugins that add extra functionality to DocPad:

- [associatedfiles](http://docpad.org/plugin/associatedfiles) - Lets you easily associate files to a particular document, and then grab the collection for them
- [buildr](http://docpad.org/plugin/buildr/) - Supports bundling scripts and styles (including pre-processors like coffeescript, less, etc) using [Buildr](https://github.com/balupton/buildr.npm)
- [cachr](http://docpad.org/plugin/cachr/) - Allows you to cache remote urls locally from within your templates
- [cleanurls](http://docpad.org/plugin/cleanurls/) - Adds support for urls like `/blog/hello` as well as the original url `/blog/hello.html`
- [csv](https://github.com/CycoPH/docpad-plugin-csv/) - Adds support for CSV data mapping. The comma seperated data files work just like a database, map from column 1 to column 2
- [dateurls](https://github.com/mgroves84/docpad-plugin-dateurls/) - Adds support for date based urls like `/2013/04/27/hello.html`
- [feedr](http://docpad.org/plugin/feedr/) - Allows you to render remote feeds within your templates
- [highlightjs](http://docpad.org/plugin/highlightjs/) - Adds [Highlight.js](https://github.com/isagalaev/highlight.js) syntax highlighting to code snippets
- [livereload](http://docpad.org/plugin/livereload) - Automatically reloads the page whenever a regeneration is performed
- [nativecomments](http://docpad.org/plugin/nativecomments/) - Adds support for native comments to DocPad
- [paged](http://docpad.org/plugin/paged/) - Adds multiple page support to documents allowing you to render one document out to many pages.
- [partials](http://docpad.org/plugin/partials/) - Adds the ability to create re-usable partials for your templates within DocPad
- [pygments](http://docpad.org/plugin/pygments/) - Adds [Pygments](http://pygments.org/) syntax highlighting to code snippets
- [related](http://docpad.org/plugin/related/) - Scans your documents `tags: 'tag1', 'tag2'` metadata to produce a listing of related documents
- [services](http://docpad.org/plugin/services/) - Adds super simple support for many 3rd party services to DocPad
- [sitemap](https://github.com/benjamind/docpad-plugin-sitemap) - Generates a `sitemap.xml` file for your site from the `html` documents collection
- [sunny](https://github.com/bobobo1618/docpad-plugin-sunny) - Uploads site to cloud (AWS, Google Storage) after generation
- [text](http://docpad.org/plugin/text/) - Render templateData properties without needing template engine, useful for abstraction in configuration files


## Deployers

These are plugins that make [deploying](/docpad/deploy) to particular services even easier:

- [ghpages](http://docpad.org/plugin/ghpages) - Deploy to [GitHub Pages](http://pages.github.com/) as easy as `docpad deploy-ghpages`


## Nifties

These are miscellaneous nifty things that you can do with DocPad:

- [Localising Dates](https://gist.github.com/4166882)
- [Automatically set custom meta data for collections](https://gist.github.com/4166806)
- [Absolute URL Helper](https://gist.github.com/3939146)
- [Benchmarking DocPad](https://gist.github.com/3906050)
- [Sitemap Generation](https://gist.github.com/3898935)
- [Concatenate your scripts with Browserify](https://gist.github.com/4398093)
- [Minify your assets with Grunt](https://gist.github.com/3898915)
- [Minify your assets automatically post-deployment with Cloudflare](http://blog.cloudflare.com/an-all-new-and-improved-autominify)
- [Custom Routing](https://gist.github.com/3695936)
- [Paging Solutions](https://gist.github.com/3695876)
- [Responsive Layouts in Stylus](https://gist.github.com/1549029)
- [Thoughts on a DocPad GUI](https://gist.github.com/2906284)
- [Getting Ruby, SASS and DocPad working on Heroku](https://gist.github.com/4342818)
- [Respond with JSON when asked to](https://github.com/lzrski/docpad-plugin-json)
- [Require authentication to view certain documents](http://stackoverflow.com/q/14327676/130638)


## Uncurated

You can find a [complete listing of all DocPad Plugins on the NPM Registry using the `docpad-plugin` keyword.](https://npmjs.org/browse/keyword/docpad-plugin) Though note, this listing is not curated by the DocPad Team, so be careful.


## Roll Your Own!

It's easy to write plugin for DocPad. [Get started now on our Write a Plugin Page!](/docpad/plugin-write)


## Requested

[Here is a list of plugins waiting to be coded up :-)](http://docpad.org/issues?labels=plugin&sort=created&direction=desc&state=open&page=1)
