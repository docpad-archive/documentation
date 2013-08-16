## Known Issues


### It just hangs after accepting the TOS or subscribing to the newsletter
It seems that this is associated to being behind a firewall or a proxy. [For the meantime, you can apply this workaround.](https://github.com/bevry/docpad/issues/488)


### I got "npm ERR! Failed to parse json"
Run your project's `package.json` file through [jsonlint](http://jsonlint.com/), there is likely to be an error somewhere in it, perhaps a missing semicolon somewhere, a missing quote?


### I'm got permission errors when I installed things
Chances are this isn't a problem within DocPad, but rather one of your node/npm installation. Run the following in Terminal, once done, try your original action again:

``` bash
sudo chown -R $USER /usr/local ~/.npm
chmod -R 755 ~/.npm
```

If that fails, we'd recommend either:

- Re-Installing Node.js with [Bevry's recommended installation instructions](http://bevry.me/node/install)
- Asking about it on the [Node.js IRC Chat Room](http://webchat.freenode.net/?channels=node.js) (`#node.js` on freenode)


### When I run `docpad run`, Windows asks me what program I would like to open the file in
It turns out that windows will prefer to treat the local `docpad.js` file as the executable versus the global `docpad.cmd` file. To get around this, type `docpad.cmd run` instead in projects that have a `docpad.js` file. [More information here.](https://github.com/bevry/docpad/issues/561#issuecomment-21494426)


### Watching doesn't work, works only some of the time, or I get `EISDIR` errors
File watching is a pretty timid thing that we are currently working on a lot to make better. There are currently two methods we can watch files, `watch` and `watchFile`. `watch` is the default and uses the operating system's watching mechanisms, however sometimes the operating system's watching mechanisms may not be the best. If that is the case, we'd like to switch our watching method to `watchFile` which is a slower, but does work when `watch` doesn't. To do this, add the following to your [docpad configuration file](/docpad/config):

``` coffee
watchOptions: preferredMethods: ['watchFile','watch']
```


### I got "We couldn't find an existing DocPad project inside your current directory..."
This occurs when you run `docpad run` inside a directory that already has existing files, but doesn't have a structure that resembles a DocPad project. We can't directly ask you if you would like to use an existing [skeleton](/docpad/skeletons) for the basis of your new website, as pulling in a skeleton inside a non-empty directory may overwrite your existing files. If would like to still use a skeleton for the basis of your new website, you will have to run docpad inside a new empty directory. If you would like to start your website from scratch (not use an existing skeleton) then you can follow the [Getting Started](/docpad/start) guide. Hope that helps :) [If you need more help then check out our Support Channels](/support).


### I'm getting "Could not locate git binary"
This happens when the [git](http://git-scm.com) installation is not exposed to your [PATH variable](http://en.wikipedia.org/wiki/PATH_%28variable%29). You can solve this in either of these two ways:

- Reinstall git and make sure to select the option during installation that asks if you would like to add it to your PATH variable (may also be called, would you like git to be available to the command line)
- Manually add the location your git binary resides in to your PATH variable

[More information about this here.](https://github.com/bevry/docpad/issues/425)


### I'm getting "EMFILE, too many open files"
As node.js is like an octopus, able to do many things at the same time, sometimes node.js will always try to do too many things than the operating system will let it. In which case, you can increase the amount of files allowed at the same time by running `ulimit -n 8192` in your terminal.


### How can I make DocPad go even faster?
There are a few things you can do:

- [Move files that you do not reference in content listings to a raw directory with the raw plugin](https://github.com/bevry/docpad/issues/276)
- [Set `standalone: true` to the meta data of documents that you regenerate often](/docpad/meta-data#standalone)
- Use native/javascript implementations of renderers instead of non-native, non-javascript ones
  - E.g. instead of using sass, use nodesass, stylus, or less
- [Help us implement performance optimisations](https://github.com/bevry/docpad/issues/529)


### I upgraded, and it doesn't work
[Check out the Upgrade Guides here](/docpad/upgrade)


### Whenever I output a variable (like `content`) it is escaped (`<` rendered as `&lt;`)?
Template engines by default _escape_ all variable output. Escaping is when we turn things like the open bracket `<` into it's _html entity_ equivalent `&lt;`. This helps prevent malicious code accidentally being injected into your website which can open the door to XSS attacks. As such, we have to use a special syntax to keep the variable _unescaped_ when outputted. The special syntax is different for the templating engine your using, so here are the ways we know:

- Eco: `<%- content %>` instead of `<%= content %>`
- Jade: `!{content}` instead of `#{content}`
- HAML: `!= content` instead of `= content`


### I get a whole bunch of npm / missing module/package / installation failed errors
If your using [Dropbox](http://j.mp/dropbox-bal) (an online syncing & backup tool) and your project is inside your DropBox folder, then click the dropbox menu icon and select "Pause Syncing". Once this is done, try whatever you were doing again, you may need to run `rm -Rf node_modules; npm install` as well. Once it's all working, then you're free to resume dropbox syncing.

If you're still experiencing issues, then be sure to post about it on the [issue tracker](/issues).


### The growl notifications aren't displaying?
I got confused by this too, turns out you need to [download and install the growlnotify extra](http://growl.cachefly.net/GrowlNotify-1.3.zip) from the [growl website](http://growl.info/). What this package does it provides command line applications the ability to call growl which is needed as docpad is a command line application.


### The exception raised by the jade plug-in during documents generation makes no sense
The jade compiler uses the full file content on the disk to show where the parsing error is. But since Docpad strips the meta header before submitting the data to the jade compiler, you must add the number of lines of this header to get the right error spot in your code.


## Need more help?

- Found a bug? [File a Bug Report on the Issue Tracker](/issues)
- Need support? [Check out our Support Channels](/support)
