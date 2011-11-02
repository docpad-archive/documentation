## Upgrading from 1.x to 2.0 (v2 is not yet released)

1. CoffeeScript v1.1.2 does not work with Node 0.5 or 0.6, so in the meantime install the older version of CoffeeScript globally `npm install -g coffee-script@1.1.1`
2. Plugins have been revised to become more future proof and configurable. Plugins must be in their own directory, with the following format: `plugins/${pluginName}/${pluginName}.plugin.coffee`
3. Plugin dependencies are no longer in the docpad or your project's `package.json`, but instead in their directory's `package.json` - e.g. `plugins/${pluginName}/package.json` - this file is optional.
4. If a plugin's `package.json` exists, as well as it's `main` property, docpad will use that as the plugin file's location instead of the location in step 2.
5. DocPad v2 brings some new features, you can read about them in the FAQ

## Upgrading from 0.x to 1.0 (v1 is the current stable version)

1. Install docpad with the new global dependences `npm install -g coffee-script docpad`
2. Any of your `documents` or `layouts` which use the eco templating engine should have the extension `.eco` appended. E.g. `layouts/default.html` to `layouts/default.html.eco`.
3. Any of your `documents` or `layouts` which utilise a markup language should have the extension `.html` prepended. E.g. `documents/something-in-markdown.md` to `documents/something-in-markdown.html.md`
4. These changes allow for some new incredibly powerful possibilities, such as allowing other templating engines other than eco, and allowing for multiple and more explicit markups to be applied to the files.