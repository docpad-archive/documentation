## Upgrading from 1.x to 2.0 (v2 is the current stable version)

1. CoffeeScript v1.1.2 does not work with Node 0.5 or 0.6, so in the meantime install the older version of CoffeeScript globally `npm install -g coffee-script@1.1.1`
2. The following steps only apply to plugin developers:
	1. Plugins have been revised to become more future proof and configurable. Plugins must be in their own directory, with the following format: `plugins/${pluginName}/${pluginName}.plugin.coffee`
	2. Plugin dependencies should no longer be in the docpad's or your project's `package.json` file, but instead in their plugin directory's `package.json` - e.g. `plugins/${pluginName}/package.json` - this file is optional, but recommended.
	3. If a plugin's `package.json` exists, as well as it's `main` property, docpad will use that as the plugin file's location instead of the location in step 2.1.
	4. Plugin configuration should be moved to their `package.json` file, to the key `docpad.plugin` which should be an object. This is then customisable by docpad's `package.json` as well as the website's via `docpad.plugin.#{pluginName}`. The configuration of a plugin is available via the `@config` property.
	5. To access docpad within a plugin, you should now use `@docpad` rather than having it passed through as an argument, this applies for logger too (now use `@logger`).
	6. A lot of docpad configuration has been moved to `@docpad.config`
3. DocPad v2 also brings a bunch of new cool features, check out the changelog on the [homepage](https://github.com/balupton/docpad) for more info, and the [FAQ](https://github.com/balupton/docpad/wiki/FAQ) for information on how to use some of these new features :-)


## Upgrading from 0.x to 1.0

1. Install docpad with the new global dependences `npm install -g coffee-script docpad`
2. Any of your `documents` or `layouts` which use the eco templating engine should have the extension `.eco` appended. E.g. `layouts/default.html` to `layouts/default.html.eco`.
3. Any of your `documents` or `layouts` which utilise a markup language should have the extension `.html` prepended. E.g. `documents/something-in-markdown.md` to `documents/something-in-markdown.html.md`
4. These changes allow for some new incredibly powerful possibilities, such as allowing other templating engines other than eco, and allowing for multiple and more explicit markups to be applied to the files.