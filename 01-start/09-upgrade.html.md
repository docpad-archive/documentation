```
title: "Upgrade Guides"
cssClasses: ['compact']
```


## Upgrade Instructions

To upgrade DocPad to the latest version, check out the latest [installation instructions](/docpad/install).

Check out the upgrade manuals below, too.


## Upgrading from 5.x to 6.x (v6 is the latest stable version)

- Configuration changes:
	- Removed the following config options: `documentsPath`, `filesPath`, and `layoutsPath`. Instead, use their array based alternatives: `documentsPaths`, `filesPaths`, `layoutsPaths`.
- Template changes:
	- Removed `require` from `templateData`. Instead, specify it in `docpad.cson` or `server.coffee`.
	- Removed `database`, `documents`, `collections`, `blocks` from `templatedata`. Instead, use their helper based alternatives: `getDatabase()`, `getCollection('documents')`, `getCollection('collectionName')`, and `getBlock('blockName')`.
- Changes affecting everyone:
	- Removed the following prototypes: `String::startsWith`, `String::finishesWith`, `Array::hasCount`, and `Array::has` (no one ever used them).
	- Plugin versions bumped to `2.x` for DocPad v6.x compatibility. In your `package.json`, you should update all plugin versions to `2.0.x` (e.g. `"docpad-plugin-eco": "2.0.x"`), then run `npm install` to install the new versions of the plugins.
- Changes affecting plugin developers:
	- Removed `docpadInstance.documents`. Instead, use `docpadInstance.getCollection('documents')`.
	- Plugin tests are now run via `npm test` on your plugin directory. Now you can use whatever test runner you want!
	- DocPad and the tester helpers have moved from Mocha to [Joe](http://github.com/bevry/joe). You'll probably want to do the same.


## Upgrading from 4.x to 5.x

1. Documents, Partials and Layouts (which extend from the `File` class) are now [Backbone Models](http://documentcloud.github.com/backbone/#Model)
	- For end-users, effects are minimal effect, as `@document` inside the `templateData` will have all the same attributes. However, any function calls will now only be accessible via the new `@documentModel`. This is because `@documentModel` is the backbone model, and `@document` is the JSONified version of the backbone model (e.g. `@document` is the same as `@documentModel.toJSON()`).
	- For plugin developers, this affects how you will retrieve and set attributes for documents. They now use the [Backbone getters and setters](http://documentcloud.github.com/backbone/#Model-get) instead of directly reading and writing attributes. E.g. `document.relatedDocuments = []` now becomes `document.set(relatedDocuments:[])` instead.

2. [Query-Engine](https://github.com/bevry/query-engine) has been updated from v0.6 to v1.1.
	- For end-users, this will have an effect wherever `@database` is used. It’s now represented by the new Query-Engine v1.1 collection, which has several changes. The most significant are that  `@database.find` is now `@database.findAll`, and they now have only a synchronous interface. E.g. `@database.findAll selector, (err,results) ->` should now be `results = @database.findAll(selector)`.
	- For plugin developers, this affects any `docpad.documents`, `docpad.partials`, and `docpad.layouts` calls. The same advice for end-users applies here, too.

3. Plugins are now handled via [npm dependencies](http://npmjs.org/doc/json.html#dependencies) instead of being directly handled by DocPad and end-users. This is the most significant change and affects everybody.
	- For end-users, you will need to add the plugins you use to your website’s `package.json` file. You can refer the [`package.json` file of the `canvas.docpad` skeleton here](https://github.com/bevry/canvas.docpad/blob/docpad-5.x/package.json#L30-43) for instructions. Once added to your website's `package.json` file, run a `npm install` to install them.
	- For plugin developers, there have been several important changes:
		1. All plugins must now have `docpad-plugin` inside the `keywords` property of their `package.json` file. It is also highly recommended to ensure your plugin’s name follows the `docpad-plugin-#{pluginName}` convention; this may become mandatory in the future.
		2. Feel free to publish plugins with `npm publish`, and add your plugin to the [Plugins wiki page](/docpad/plugins) so others can install it themselves (e.g. `npm install docpad-plugin-#{pluginName}`)!

If you have any problems be sure to report them on the [Issue Tracker](/issues). Thanks.


## Upgrading from 3.x to 4.x

1. Skeletons are no longer cached, which means that you can no longer create a new website using a skeleton while offline. While this can be a pain, it necessary to improve stability and reduce complexity of the code base.

2. A document's `title` will no longer default to the document's `filename` if unset. Instead, a new property called `name` exists, which can be set by your document meta data. (This allows the `title` property to be used for Page `<title>`s, whereas the `name` property can be used for navigation listings, etc.)

3. The DocPad core has been cleaned up a lot—and as such, so has the way plugin events are triggered. We now utilise [balUtil's](https://github.com/balupton/bal-util.npm) [emitSync](https://github.com/balupton/bal-util.npm/blob/master/lib/events.coffee#L257) and [emitAsync](https://github.com/balupton/bal-util.npm/blob/master/lib/events.coffee#L241) instead of the old `triggerPluginEvent`. This means that (for now) plugin priorities are discarded; however, they may return in the future (so leave them in there if you have them!).

4. Plugin rendering has had a significant change: you should no longer use `file.content` to read and update the current document's content. Instead, a new argument called `content` will be passed, and it should be written to as well. **This is a breaking change**, and all renderers must be updated accordingly. To learn the new way, then check out the [Extending DocPad](/docpad/extend) wiki page.

5. Errors are now sent back to DocPad using the [AirBrake](http://airbrake.io) service. If you would like this disabled, turn it off by setting `reportErrors` to `false` in your DocPad configuration.

6. A lot of unstable or not-so-popular plugins have been moved into the new [docpad-extras](https://github.com/bevry/docpad-extras) repository. The plugins moved are: `admin`, `authenticate`, `autoupdate`, `buildr`, `html2jade`, `move`, `php`, `rest`, `roy`, and `ruby`. If you would like to continue using them, you’ll have to download them manually from the `docpad-extras` repository and insert them into your website's `plugins` directory.


## Upgrading from 2.x to 3.x

1. The `File` class has had lots of properties renamed. The `File` class is used for all documents and layouts, which would likely affect you when rendering properties from documents inside your templates (e.g. `@document.title`). This change was made to better correlate the names with their values; previously, the correlation was quite ambiguous. [You can find the current set of properties and their descriptions here.](https://github.com/bevry/docpad/blob/master/lib/file.coffee#L12)

2. For plugin developers, the way you extend from the `BasePlugin`, and the way you `module.exports` your plugin has changed. [To learn about the new convention, refer to the new _Extending_ guide by clicking here.](/docpad/extend)

3. For those using DocPad as a module, it now supports a `next` callback on its constructor, allowing you to do `new DocPad(config,next)`. Anything that depends on a DocPad action being completed should go inside the `next` callback. While optional, it has provided helpful in eliminating timing problems.

## Upgrading from 1.x to 2.x

1. CoffeeScript v1.1.2 does not work with Node 0.5 or 0.6; you have to use v1.1.3 or higher. To do this, re-install CoffeeScript with `npm install -g coffee-script`.
2. For plugin developers:
	1. Plugins have been revised to become more future-proof and configurable. Plugins must be in their own directory, with the following format: `plugins/${pluginName}/${pluginName}.plugin.coffee`.
	2. Plugin dependencies should no longer be in DocPad's (or your project's) `package.json` file, but rather in their own directory's `package.json` (e.g. `plugins/${pluginName}/package.json`). This file is optional, but recommended.
	3. If a plugin's `package.json` exists, as well as its `main` property, DocPad will use that as the plugin file's location instead of the location in step 2.1.
	4. Plugin configuration should be moved to their `package.json` file, to the key `docpad.plugin`, which should be an object. This is then customisable by DocPad's `package.json` (use `docpad.plugin.#{pluginName}` on the website). The configuration of a plugin is available via the `@config` property.
	5. To access DocPad within a plugin, you should use `@docpad` rather than having it passed as an argument. The same goes for the logger (use `@logger`).
	6. Lots of DocPad configuration has been moved to `@docpad.config`
3. DocPad v2 also brings a bunch of new cool features! Check out the changelog on the [homepage](https://github.com/balupton/docpad) for more info, and the [FAQ](https://github.com/balupton/docpad/wiki/FAQ) for information on how to use some of these new features. :-)
4. The Bootstrap Skeleton is now the [Kitchensink Skeleton](https://github.com/balupton/kitchensink.docpad)


## Upgrading from 0.x to 1.x

1. Install DocPad with the new global dependences `npm install -g coffee-script docpad`
2. Any of your `documents` or `layouts` which use the eco templating engine should have the extension `.eco` appended. E.g. `layouts/default.html` to `layouts/default.html.eco`.
3. Any of your `documents` or `layouts` which utilise a markup language should have the extension `.html` prepended. E.g. `documents/something-in-markdown.md` to `documents/something-in-markdown.html.md`
4. These changes allow for some new incredibly powerful possibilities, such as allowing other templating engines other than eco, and allowing for multiple and more explicit markups to be applied to the files.