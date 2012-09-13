The DocPad configuration file sits within the root of your DocPad project and be named as one of the following. Each name provides a special meaing. Here are the valid names:

- `docpad.js` a node javascript file, will generally look like: `module.exports = {/*the configuration*/}`
- `docpad.json` a json file, does not allow functions, will generally look like: `{/*the configuration*/}`
- `docpad.coffee` a node coffeescript file, will generally look like: `module.exports = /*the configuration*/`
- `docpad.cson` a [cson](https://github.com/bevry/cson) file, will generally look like: `/*the configuration*/`

The advantage of `docpad.js` and `docpad.coffee` over `docpad.json` and `docpad.cson` is that they allow us to declare functions, as well as call functions. However, for instances where we cannot trust the contents of the configuration files you would want to use the `docpad.json` or `docpad.cson` as they can't do anything naughty.

The advantage of `docpad.coffee` and `docpad.cson` over `docpad.js` and `docpad.json` is that they allow us to use the CoffeeScript syntax which is a lot more leaniant.

Generally, you'll usually always find either a `docpad.coffee` file or a `docpad.cson` file.