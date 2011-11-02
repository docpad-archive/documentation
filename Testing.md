So you want to try out the latest and greatest DocPad version, we could sure do with the help! :D


## Warning

**You are about to install a non-stable version of docpad, so shit will probably break... this is good because we can file a bug report and it can get fixed. Although it is bad if we forgot to backup... Remember to always backup, use dropbox, or use git to ensure all the necessary safety measures are in place. All safe? Great, let's move on.**


## Pre-Requisites

- DocPad v2 should run both Node.js 0.4 and 0.5/0.6, if you can test them both that would be amazing. As well as on Mac and Windows. To run multiple versions of node.js on the same machine you can use [NVM](https://github.com/creationix/nvm) - though be sure to UNINSTALL your original node.js before install NVM, as well as removing NODE_PATH from your dot profiles.


## Installing

``` bash
git clone git://github.com/balupton/docpad.git
cd docpad
git fetch origin
git checkout dev
npm install -g coffee-script@1.1.1
npm install
git submodule init
git submodule update
npm link
```


## Using

- The above installation instructions will have setup the global `docpad` command line tool
- If you are wanting to do something like `docpad = require('docpad')` then you'll have to do a `npm link docpad` inside your project's directory


## Upgrading

- Be sure to checkout the [upgrade guides](https://github.com/balupton/docpad/wiki/Upgrading)


## Testing

Try it out on your existing docpad website, or on a new one, try and break it, and find out what happens. Report any problems or feature requests to the [issue tracker](https://github.com/balupton/docpad/issues)


## Things still to come

- Specifying that we only want to load certain plugins
- Plugin specific configurations via `package.json` files


## Where does this release fit in?

Check the [roadmap](https://github.com/balupton/docpad/wiki/Roadmap)


## Thanks

Love you guys! I really do appreciate all the help! You seriously rock!