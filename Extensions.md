It's interesting to see what plugins others have come up with. Link to DocPad plugins here.

## Core

These plugins are already bundled with DocPad. This means their included by default :-)

### Renderers

- [Markdown Plugin](https://github.com/balupton/docpad/blob/master/lib/plugins/renderers/markdown.plugin.coffee) - supports [Markdown](ttp://daringfireball.net/projects/markdown/basics) to HTML
- [Coffee Plugin](https://github.com/balupton/docpad/blob/master/lib/plugins/renderers/coffee.plugin.coffee) - supports [CoffeeKup](http://coffeekup.org/) to anything and from HTML, and [CoffeeScript](http://jashkenas.github.com/coffee-script/) to and from JavaScript
- [Eco Plugin](https://github.com/balupton/docpad/blob/master/lib/plugins/renderers/eco.plugin.coffee) - supports [Eco](https://github.com/sstephenson/eco) to anything
- [Jade Plugin](https://github.com/balupton/docpad/blob/master/lib/plugins/renderers/jade.plugin.coffee) - supports [Jade](http://jade-lang.com/) to anything
- [HAML Plugin](https://github.com/balupton/docpad/blob/master/lib/plugins/renderers/haml.plugin.coffee) - supports [HAML](http://haml-lang.com/) to anything
- [Stylus Plugin](https://github.com/balupton/docpad/blob/master/lib/plugins/renderers/stylus.plugin.coffee) - supports [Stylus](http://learnboost.github.com/stylus/) to CSS

### Helpers

- [Buildr Plugin](https://github.com/balupton/docpad/blob/master/lib/plugins/helpers/buildr.plugin.coffee) - Supports bundling scripts and styles (including pre-processors like coffeescript, less, etc) using [Buildr](https://github.com/balupton/buildr.npm)
- [Clean Urls Plugin](https://github.com/balupton/docpad/blob/master/lib/plugins/helpers/cleanurls.plugin.coffee) - adds support for urls like `/blog/hello` as well as the original url `/blog/hello.html`
- [Related Pages Plugin](https://github.com/balupton/docpad/blob/master/lib/plugins/helpers/relations.plugin.coffee) - scans your documents `tags: 'tag1', 'tag2'` metadata to produce a listing of related documents. Access them through `@document.relatedDocuments`


## User Created

These plugins you'll have to install manually.

- None yet, start creating!


## Waiting to be implemented

[Here is a list of plugins waiting to be coded up :-)](https://github.com/balupton/docpad/issues?labels=plugin&sort=created&direction=desc&state=open&page=1)