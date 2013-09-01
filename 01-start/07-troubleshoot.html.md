## Known Issues


### It just hangs after accepting the TOS or subscribing to the newsletter
It seems that this is associated to being behind a firewall or a proxy. [For the meantime, you can apply this workaround.](https://github.com/bevry/docpad/issues/488)


### I got `npm ERR! Failed to parse json`
Run your project's `package.json` file through [jsonlint](http://jsonlint.com/), there is likely to be an error somewhere in it, perhaps a missing semicolon somewhere, a missing quote?


### I got permission errors when I try to install things
Chances are this isn't a problem within DocPad, but with your installation of node or npm. Run the following in Terminal and try again:

``` bash
sudo chown -R $USER /usr/local ~/.npm
chmod -R 755 ~/.npm
```

If that fails, either:

- Re-Installing Node.js with [Bevry's recommended installation instructions](http://bevry.me/node/install)
- Asking about it on the [Node.js IRC Chat Room](http://webchat.freenode.net/?channels=node.js) (`#node.js` on freenode)


### When I run `docpad run`, Windows asks me what program I would like to open the file in
It turns out that Windows will prefer to treat the local `docpad.js` file as the executable (instead of the global `docpad.cmd`). To get around this, type `docpad.cmd run` in projects with a `docpad.js` file. [More information here.](https://github.com/bevry/docpad/issues/561#issuecomment-21494426)


### Watching «doesn't work/works only sometimes/gives `EISDIR` errors»
File watching is a pretty timid thing. We’re currently working on making it better. There are currently two methods we use to watch files: `watch` and `watchFile`. 

- `watch` is the default and uses the operating system's watching mechanisms. However, sometimes the operating system's watching mechanisms aren’t the best. If that’s the case, we'd like to switch to...
- `watchFile`! It’s slower, but it works when `watch` doesn’t. 

To do this, add the following to your [docpad configuration file](/docpad/config):

``` coffee
watchOptions: preferredMethods: ['watchFile','watch']
```


### I got `We couldn't find an existing DocPad project inside your current directory...`
This occurs when you run `docpad run` in a directory that already has existing files, but doesn't have a structure that resembles a DocPad project. We can't directly ask you if you would like to use an existing [skeleton](/docpad/skeletons) for the basis of your new website, as pulling in a skeleton inside a non-empty directory might overwrite your existing files. 

If you want to still use a skeleton for the basis of your new website, run DocPad inside a new empty directory. 

If you want to start your website from scratch (not use an existing skeleton), follow the [Getting Started](/docpad/start) guide. Hope that helps :) 

[If you need more help then check out our Support Channels](/support).


### I'm getting `Could not locate git binary`
This happens when the [git](http://git-scm.com) installation is not exposed to your [PATH variable](http://en.wikipedia.org/wiki/PATH_%28variable%29). You can solve this in one of two ways:

- Reinstall `git`, and be sure to select the option during installation that asks if you would like to add it to your `PATH` variable (sometimes worded “...to the command line”)
- Manually add git’s location to your `PATH` variable

[More information about this here.](https://github.com/bevry/docpad/issues/425)


### I'm getting `EMFILE, too many open files`
Node.js is like an octopus—able to do many things at the same time. Sometimes Node.js tries to do more things than the operating system allows at once. In that case, you can tell the operating system to allow more simultaneous open files  by running `ulimit -n 8192` in your terminal.


### How can I make DocPad go even faster?
There are a few things you can do:

- [Move files that you do not reference in content listings to a raw directory with the raw plugin](https://github.com/bevry/docpad/issues/276)
- [Set `standalone: true` to the meta data of documents that you regenerate often](/docpad/meta-data#standalone)
- Use native/javascript implementations of renderers instead of non-native, non-javascript ones. (E.g. use `stylus` or `less`; or, use `nodesass` instead of `sass`.)
- [Help us implement performance optimisations](https://github.com/bevry/docpad/issues/529)


### I upgraded, and DocPad broke
[Check out the Upgrade Guides here](/docpad/upgrade)


### Whenever I output a variable (like `content`), it’s escaped (`<` rendered as `&lt;`)
Template engines by default _escape_ all variable output. Escaping is when we turn things like the open bracket `<` into its _html entity_ equivalent `&lt;`. This helps prevent malicious code accidentally being injected into your website, which could allow XSS attacks. 

As such, we have to use a special syntax to keep the variable _unescaped_ when outputted. The special syntax is different for the templating engine your using, so here are the ways we know:

- Eco: `<%- content %>` instead of `<%= content %>`
- Jade: `!{content}` instead of `#{content}`
- HAML: `!= content` instead of `= content`


### I get a whole bunch of npm / missing module/package / installation failed errors
If you’re using [Dropbox](http://j.mp/dropbox-bal), and your project is inside your DropBox folder, then click the DropBox menu icon and select "Pause Syncing". Then try again; you may need to run `rm -Rf node_modules; npm install` as well. 

Once it's all working, you can resume dropbox syncing.

If you're still experiencing issues, then be sure to post about it on the [issue tracker](/issues).


### The growl notifications aren't displaying
You need the [`growlnotify` extra](http://growl.cachefly.net/GrowlNotify-1.3.zip) from the [growl website](http://growl.info). This nifty little package provides command line applications the ability to call growl. (I got confused by this, too.)


### The exception raised by the jade plug-in during documents generation makes no sense
The jade compiler uses the full file content on the disk to show where the parsing error is. However, since DocPad strips the meta header before sending the data to jade, the reported line numbers will be off by the length of your header.  

To get the correct line number, just add the length of your header (in lines) to the reported line number.


## Need more help?

- Found a bug? [File a Bug Report on the Issue Tracker](/issues)
- Need support? [Check out our Support Channels](/support)
