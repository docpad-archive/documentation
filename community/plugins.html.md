Here's a list of all available DocPad plugins. If you've created a plugin, be sure to [include it in this listing!](https://github.com/docpad/documentation/edit/master/community/plugins.html.md) :)


## Installing

To install a plugin, run `docpad install #{thePluginName}` inside your project directory. As an example, to install the [eco](https://github.com/docpad/docpad-plugin-eco/) plugin, you would run `docpad install eco`

To uninstall a plugin, run `docpad uninstall #{thePluginName}` inside your project directory.

In older versions of DocPad, you would run `npm install --save docpad-plugin-#{thePluginName}` to install, and `npm uninstall --save docpad-plugin-#{thePluginName}` to uninstall.


## Renderers

These are plugins that add support for extra markups and languages to DocPad:

### Writing Markups
- [marked](https://github.com/docpad/docpad-plugin-marked/) - Supports [Markdown](http://daringfireball.net/projects/markdown/basics) to HTML `.html.(md|markdown)` via [marked](https://github.com/chjj/marked)
- [orgmode](https://bitbucket.org/bgschaid/docpad-plugin-orgmode/) - Supports converting  [org-mode](http://orgmode.org) to HTML `.html.org` via [org-js](https://github.com/mooz/org-js)
- [textile](https://github.com/Greduan/docpad-plugin-textile) - Supports [Textile](https://www.npmjs.com/package/textile-js) to HTML `.html.textile`
- [markit](https://github.com/tbusser/docpad-plugin-markit) - Supports [Markdown](http://daringfireball.net/projects/markdown/basics) to HTML `.html.(md|markdown)` via [markdown-it](https://github.com/markdown-it/markdown-it)
- [asciidoc](https://github.com/fboulay/docpad-plugin-asciidoc) - Supports [Asciidoc](http://asciidoctor.org/docs/what-is-asciidoc/) to HTML `.html.adoc` via [asciidoctor.js](https://github.com/asciidoctor/asciidoctor.js)

### Data Markups
- [cson](https://github.com/docpad/docpad-plugin-cson/) - Supports [CSON](https://github.com/bevry/cson) to JSON `.json.cson`
- [yaml](https://github.com/jeremyfa/docpad-plugin-yamljs) - Supports [YAML](http://en.wikipedia.org/wiki/YAML) to JSON `.json.(yaml|yml)` and JSON to YAML `.(yml|yaml).json`

### CSS Pre-Processors
- [less](https://github.com/docpad/docpad-plugin-less/) - Supports [LessCSS](http://lesscss.org) to CSS `.css.less`
- [roole](https://github.com/georgeosddev/docpad-plugin-roole) - Supports [Roole](http://roole.org) to CSS `.css.roo`
- [sass](https://github.com/docpad/docpad-plugin-sass/) - Supports [SCSS and SASS](http://sass-lang.com) to CSS (includes [compass](http://compass-style.org) support) `.css.(sass|scss)`
- [nodesass](https://github.com/docpad/docpad-plugin-nodesass) - Supports [SCSS](http://sass-lang.com) to CSS (using [node-sass](https://github.com/andrew/node-sass)) `.css.scss`
- [styl](https://github.com/docpad/docpad-plugin-styl/) - Supports [Styl](https://github.com/visionmedia/styl) to CSS `.css.styl`
- [stylus](https://github.com/docpad/docpad-plugin-stylus/) - Supports [Stylus](http://learnboost.github.com/stylus/) to CSS `.css.(styl|stylus)`

### Javascript Pre-Processors
- [coffeescript](https://github.com/docpad/docpad-plugin-coffeescript/) - Supports [CoffeeScript](http://coffeescript.org/) to JavaScript `.js.coffee`
- [js2coffee](https://npmjs.org/package/docpad-plugin-js2coffee) - Supports JavaScript to CoffeeScript `.coffee.js`
- [livescript](https://github.com/docpad/docpad-plugin-livescript/) - Supports [LiveScript](http://livescript.net) to JavaScript `.js.ls`
- [move](https://github.com/docpad/docpad-plugin-move) - Supports [Move](https://github.com/rsms/move) to JavaScript `.js.move`
- [typescript](https://github.com/bpampuch/docpad-plugin-tsc) - Supports [TypeScript](http://www.typescriptlang.org) to JavaScript `.js.ts`
- [babel](https://github.com/williammalo/docpad-plugin-babel/) - Supports ES6 to JavaScript using [Babel](http://babeljs.io/) `.js.babel`
- [traceur](https://github.com/pflannery/docpad-plugin-traceur/) - Supports ES6 to JavaScript using [Traceur](https://github.com/google/traceur-compiler) `.js.traceur`

### HTML Pre-Processors

#### CoffeeScript Templating Engines
- [eco](https://github.com/docpad/docpad-plugin-eco/) - Supports [Eco](https://github.com/sstephenson/eco) to anything `.anything.eco`
- [coffeekup](https://github.com/docpad/docpad-plugin-coffeekup/) - Supports [CoffeeKup](http://coffeekup.org) to anything `.anything.coffee`
- [html2coffee](https://github.com/docpad/docpad-plugin-html2coffee/) - Supports HTML to CoffeeKup `.coffee.html`
- [coffeemugg](https://github.com/pflannery/docpad-plugin-coffeemugg) - Supports [CoffeeMugg](https://github.com/jaekwon/CoffeeMugg)  to anything `.anything.coffee`
- [hamlcoffee](https://github.com/ashnur/docpad-plugin-hamlcoffee/) - Supports [Haml Coffee](https://github.com/netzpirat/haml-coffee/) to HTML `.html.hamlc`
- [teacup](https://github.com/hurrymaplelad/docpad-plugin-teacup/) - Supports [Teacup](http://goodeggs.github.io/teacup/) to HTML `.html.coffee`
- [without](https://github.com/ukoloff/docpad-plugin-without) - Supports [withOut](https://github.com/ukoloff/without) to HTML `.html.coffee`

#### HAML-Like Templating Engines
- [haml](https://github.com/docpad/docpad-plugin-haml/) - Supports [Haml](http://haml.info) to anything `.anything.haml`
- [jade](https://github.com/docpad/docpad-plugin-jade/) - Supports [Jade](http://jade-lang.com) to anything `.anything.jade`
- [html2jade](https://github.com/docpad/docpad-plugin-html2jade) - Supports HTML to [Jade](http://jade-lang.com) `.jade.html`

#### Moustache Templating Engines
- [handlebars](https://github.com/docpad/docpad-plugin-handlebars/) - Supports [Handlebars/Moustache](http://handlebarsjs.com) to anything `.anything.(hb|hbs|handlebars)`
- [hogan](https://github.com/docpad/docpad-plugin-hogan/) - Supports [Hogan/Mustache](http://twitter.github.io/hogan.js/) to anything `.anything.hogan`

#### Other Templating Engines
- [consolidate](http://github.com/robloach/docpad-plugin-consolidate) - Supports many template engines via [Consolidate.js](https://github.com/visionmedia/consolidate.js)
- [slim](https://github.com/patocallaghan/docpad-plugin-slim) - Supports [Slim](http://slim-lang.com) to anything `.anything.slim`
- [swig](https://github.com/thisispete/docpad-plugin-swig) - Supports [Swig](https://github.com/paularmstrong/swig/) to HTML `.html.swig`
- [htmlmin](http://github.com/robloach/docpad-plugin-htmlmin) - Supports minifying HTML with [HTML-Minifier](http://kangax.github.io/html-minifier/) `.html.anything`
- [vash](https://github.com/harmony7/docpad-plugin-vash) - Supports [Vash](https://github.com/kirbysayshi/vash), an implementation of the [Razor template syntax](http://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) for JavaScript, to anything `.anything.vash`

### Languages
- [cmds](https://github.com/pflannery/docpad-plugin-cmds/) - Adds some shell scripting fun. Supports `.anything.bash|.anything.sh|.anything.ps1|.anything.cmd`
- [php](https://github.com/docpad/docpad-plugin-php) - Supports [PHP](http://php.net) to anything `.anything.(php|phtml)`
- [ruby](https://github.com/docpad/docpad-plugin-ruby) - Supports [Ruby](http://www.ruby-lang.org) and [ERuby](http://en.wikipedia.org/wiki/ERuby) to anything `.anything.(ruby|erb)`


## Helpers

These are plugins that add extra functionality to DocPad:

- [addthis](https://github.com/mikeumus/docpad-plugin-addthis) - Adds the [AddThis](http://www.addthis.com) toolbar into your project
- [assets](https://github.com/mcdee/docpad-plugin-assets) - Change URL of asset files to contain hash of contents, allowing for effective caching whilst enabling cache busting when contents change
- [associatedfiles](https://github.com/docpad/docpad-plugin-associatedfiles) - Lets you easily associate files to a particular document, and then grab the collection for them
- [authentication](https://github.com/SteveMcArthur/docpad-plugin-authentication) - Handles authentication and login functionality via social login (ie google, facebook, twitter or github) for your docpad application. Protects pages from unauthenticated users.
- [basicauth](https://github.com/mikeumus/docpad-plugin-basicauth) - Adds basic authentication to your project
- [browserifybundles](https://github.com/docpad/docpad-plugin-browserifybundles) - Add configuration to your DocPad configuration file to create browserify bundles of your scripts
- [browserifydocs](https://github.com/docpad/docpad-plugin-browserifydocs) - Browserify your documents by adding `browserify: true` to their meta data
- [buildr](https://github.com/docpad/docpad-plugin-buildr/) - Supports bundling scripts and styles (including pre-processors like CoffeeScript, LESS, etc.) using [Buildr](https://github.com/balupton/buildr)
- [cachr](https://github.com/docpad/docpad-plugin-cachr/) - Allows you to cache remote URLs locally from within your templates
- [cleancss](https://github.com/docpad/docpad-plugin-cleancss) - Concatinate and minify CSS files with the `cleancss: true` meta data
- [cleanurls](https://github.com/docpad/docpad-plugin-cleanurls/) - Adds support for URLs like `/blog/hello` as well as the original URL `/blog/hello.html`
- [coffeelint](https://github.com/docpad/docpad-plugin-coffeelint) - Prints [coffeelint](http://www.coffeelint.org) errors to the console
- [csv](https://github.com/CycoPH/docpad-plugin-csv/) - Adds support for CSV data mapping. The comma seperated data files work just like a database, map from column 1 to column 2
- [datefromfilename](https://github.com/grassator/docpad-plugin-datefromfilename) - Automaticaly set the `date` meta-data property by determining it from the document's filename
- [dateurls](https://github.com/mgroves84/docpad-plugin-dateurls/) - Adds support for date-based URLs like `/2013/04/27/hello.html`
- [facebookcomments](https://github.com/mikeumus/docpad-plugin-facebookcomments) - Adds the [Facebook Comment Widget](https://developers.facebook.com/docs/reference/plugins/comments/) to your project
- [feedr](https://github.com/docpad/docpad-plugin-feedr/) - Allows you to render remote feeds within your templates
- [frontend](https://npmjs.org/package/docpad-plugin-frontend) - CSS and JavaScript asset manager and compiler for DocPad
- [functions](https://www.npmjs.com/package/docpad-plugin-functions) - Start functions between DocPad events
- [gist](https://github.com/docpad/docpad-plugin-gist/)  - Pulls in gists into your document
- [grunt](http://github.com/robloach/docpad-plugin-grunt) - Run [Grunt.js](http://gruntjs.com) tasks when building with DocPad
- [heapdumper](https://github.com/pflannery/docpad-plugin-heapdumper) - Generates a heapdump snapshot for chosen DocPad event(s), viewable in the Chrome profiler
- [highlightjs](https://github.com/docpad/docpad-plugin-highlightjs/) - Adds [Highlight.js](https://github.com/isagalaev/highlight.js) syntax highlighting to code snippets
- [ignoreincludes](https://github.com/rantecki/docpad-plugin-ignoreincludes) - Avoid writing include files to the `/out` directory
- [jsexc](https://github.com/JeffreyZhao/docpad-plugin-jscexc) - Adds the ability to apply AOT compilation to JavaScript files
- [jshint](https://github.com/docpad/docpad-plugin-jshint) - Prints [JSHint](http://www.jshint.com) errors to the console
- [jsonfragment](https://github.com/field/docpad-plugin-jsonfragment) - Writes each documents content without layout and its meta data into a separate `.json` file for quick loading via AJAX.
- [livereload](https://github.com/docpad/docpad-plugin-livereload) - Automatically reloads the page whenever a regeneration is performed
- [lunr](https://github.com/brockfanning/docpad-plugin-lunr) - Client-side full-text and faceted search using [Lunr.js](http://lunrjs.com)
- [menu](https://github.com/sergeche/docpad-plugin-menu) - Automatically generates menu from `/render` folder
- [moment](https://github.com/brockfanning/docpad-plugin-moment) - Date formatting and access to [Moment.js](http://momentjs.com) library
- [nativecomments](https://github.com/docpad/docpad-plugin-nativecomments/) - Adds support for native comments to DocPad
- [navlinks](https://github.com/lucor/docpad-plugin-navlinks) - Adds the ability to generate a navigation bar for documents with links to the next and previous document of a specified collection.
- [paged](https://github.com/docpad/docpad-plugin-paged/) - Adds multiple page support to documents allowing you to render one document out to many pages
- [partials](https://github.com/docpad/docpad-plugin-partials/) - Adds the ability to create re-usable partials for your templates within DocPad
- [pygments](https://github.com/docpad/docpad-plugin-pygments/) - Adds [Pygments](http://pygments.org) syntax highlighting to code snippets
- [raw](https://github.com/docpad/docpad-plugin-raw) - Copies all files in the `/raw` directory to `/out` without going through DocPad's generation process. Useful for files that cause out of memory/speed issues when placed in `/static` directory.
- [copy](https://github.com/almero-digital-marketing/docpad-plugin-copy) - Alternative to raw pluging with performace optimizations. Copies all files in the `/raw` directory to `/out` without going through DocPad's generation process. Useful for files that cause out of memory/speed issues when placed in `/static` directory.
- [react](https://github.com/chrishale/docpad-plugin-react) - Renders markup for [React](http://facebook.github.io/react/) Components
- [redirector](https://github.com/nfriedly/docpad-plugin-redirector) - Creats redirects (301 or meta-refresh) via configuration.
- [related](https://github.com/docpad/docpad-plugin-related/) - Scans your documents `tags: 'tag1', 'tag2'` metadata to produce a listing of related documents
- [rss](https://github.com/hurrymaplelad/docpad-plugin-rss) - Generates an RSS feed for a configurable collection
- [scheduling](https://github.com/miletbaker/docpad-plugin-scheduling) - Schedules content so that it is not rendered out before the ```date``` specified in the content's meta-data.
- [schema](https://www.npmjs.com/package/docpad-plugin-schema) - Adds support for JSON schema in DocPad collections
- [services](https://github.com/docpad/docpad-plugin-services/) - Adds support for many 3rd party services to DocPad
- [shortcodes](https://github.com/field/docpad-plugin-shortcodes) - Adds various Wordpress style shortcodes (e.g., `[video id="123"]`) to simplify template writing.
- [sitemap](https://github.com/benjamind/docpad-plugin-sitemap) - Generates a `sitemap.xml` file for your site from the `html` documents collection
- [tableofcontents](https://github.com/takitapart/docpad-plugin-tableofcontents) - Automatically generate table of contents
- [text](https://github.com/docpad/docpad-plugin-text/) - Render `templateData` properties without needing template engine, useful for abstraction in configuration files
- [thumbnails](https://github.com/rantecki/docpad-plugin-thumbnails) - Manages thumbnail generation of your image files
- [imagedimensions](https://github.com/knoblochtobias/docpad-plugin-imagedimensions) - Get the size of in image in your static files.
- [imagin](https://github.com/almero-digital-marketing/docpad-plugin-imagin) - Alternative to thumbails plugin with support for `raw` and `copy` plugins for performance optimization. Manages thumbnail generation of your image files.
- [tinylivereload](https://github.com/andruhon/docpad-plugin-tinylivereload) - A LiveReload plugin that doesn't alter your HTML. Works with the Chrome/Firefox LiveReload extensions.
- [uglify](https://github.com/docpad/docpad-plugin-uglify) - Compress and minify JavaScript files with the `uglify: true` meta data
- [umd](https://github.com/docpad/docpad-plugin-umd/) - Wrap specified JavaScript documents in the Universal Module Definition (UMD) allowing them to run in AMD, Require.js, CommonJS/Node.js and Vanilla environments automatically
- [sanitizer](https://github.com/kennyki/docpad-plugin-sanitizer) - A helper for HTML string sanitization based on Google Caja


## Deployers

These are plugins that make [deploying](https://docpad.org/docs/deploy) to particular services even easier:

- [ghpages](https://github.com/docpad/docpad-plugin-ghpages) - Deploy to [GitHub Pages](http://pages.github.com) as easy as `docpad deploy-ghpages`
- [sunny](https://github.com/bobobo1618/docpad-plugin-sunny) - Uploads site to cloud (AWS, Google Storage) after generation



## Admin Interfaces

[DocPad's plan from the very beginning has been to be interface agnostic.](https://github.com/bevry/docpad/issues/123) This means that we will be able to utilise existing interfaces, customer interfaces, and decoupled interfaces. Allowing us to always utilise the best experiences for everyone involved.


### Existing Interfaces
<a id="importers"></a>

DocPad's plugin/extension infrastructure supports existing coupled interfaces by importing their data directly into the DocPad Database. So if you love using Tumblr, WordPress, Medium, MongoDB, or GitHub repos for your content, you don't have to give them up. Just install the importer plugin for them, and DocPad will import the data from that service into the DocPad database for rendering.

- [downloader](https://github.com/docpad/docpad-plugin-downloader/) - Download (and optionally extract) files into your project, used in the [Bootstrap Skeleton](https://github.com/docpad/twitter-bootstrap.docpad) to pull in [Bootstrap](http://getbootstrap.com/)
- [repocloner](https://github.com/docpad/docpad-plugin-repocloner/) - Clone repos into your project, awesome for [creating wikis](https://gist.github.com/balupton/5519403)
- [tumblr](https://github.com/docpad/docpad-plugin-tumblr/) - Imports Tumblr data directly into your DocPad Database, used in the [Syte Skeleton](https://github.com/docpad/syte.docpad) to pull in Tumblr data
- [mongodb](https://github.com/nfriedly/docpad-plugin-mongodb) - Imports collections from MongoDB.
- [cloudant](https://github.com/nfriedly/docpad-plugin-cloudant) - Imports collections from Cloudant (CouchDB)


### Custom Interfaces

DocPad's plugin/extension infrastructure supports custom Admin Interfaces tightly coupled to the DocPad experience. So far we have the following extensions that add Admin Interfaces to DocPad:

- [DocPad Collections Editor](https://github.com/cauld/docpad-collections-editor) - A simple WYSIWYG editor for DocPad Collections
- [MiniCMS](https://npmjs.org/package/docpad-plugin-minicms) - Adds an admin interface to DocPad
- [CMS Docpad](https://github.com/Reaktivate/docpad-cms) - Lightweight CMS UI with WYSIWYG editor for pages and parts

### Decoupled Interfaces

DocPad's plugin/extension infrastructure supports existing decoupled interfaces by providing plugin/extension adapters to the interface allowing the interface to interact directly with the DocPad Database, or theoretically any backend providing an interface was made for it. So far we have the following extensions that add Decoupled Interfaces to DocPad:

- [Use Prose with DocPad to create a Wiki](https://gist.github.com/balupton/5519403) - Tutorial on how to use [Prose.io](http://prose.io/#about) as an Admin Interface for DocPad
- [WebWrite's InlineGUI](https://github.com/docpad/docpad-plugin-inlinegui) (not yet ready) - Edit your content from any backend with this inline editing interface
- [Edit & Deploy with GitHub.com & GHpages Plugin](https://github.com/Sun-Star-IT/sunstarit.docpad/wiki/Edit-&-Deploy-with-GitHub.com-&-GHpages-Plugin) - Wiki on how to use GitHub.com to edit your DocPad website and then DocPad's `ghpages` plugin to deploy to GitHub Pages.


## Guides

These are miscellaneous things that you can do with DocPad:

- [Localising and formatting dates](https://gist.github.com/4166882)
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
- [Use DocPad and GitHub as a Wiki](https://gist.github.com/balupton/5519403)



## Complete Plugin Listing

You can find a [complete listing of all DocPad Plugins on the NPM Registry using the `docpad-plugin` keyword.](https://www.npmjs.com/browse/keyword/docpad-plugin) Though note, this listing is not curated by the DocPad Team, so be careful.



## Create Your Own!

It's easy to write plugin for DocPad. [Get started now on our Write a Plugin Page!](https://docpad.org/docs/plugin-write)
