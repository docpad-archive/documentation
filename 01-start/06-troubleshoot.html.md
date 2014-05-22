## Known Issues


### Regressions we’re working on
The following are issues the DocPad team are aware of and will fix shortly:

- Dynamic pages are behaving weirdly: https://github.com/bevry/docpad/issues/767
- Ignored documents are showing up in collections and being served: https://github.com/bevry/docpad/issues/807


### It just hangs after accepting the TOS or subscribing to the newsletter
It seems that this is associated to being behind a firewall or a proxy. You can apply [this workaround](https://github.com/bevry/docpad/issues/488).


### I got “npm ERR! Failed to parse json”
Check your project’s `package.json` file with [JSONLint](http://jsonlint.com/), to ensure it does not contain any errors, such as missing semicolons, quotes or commas.


### I am getting permission errors after I install things
Chances are this isn’t a problem within DocPad, but rather one of your Node/NPM installations. Run the following in Terminal, once done, try your original action again:

``` bash
sudo chown -R $USER /usr/local ~/.npm
chmod -R 755 ~/.npm
```

Be sure that your tmp dir is writable for the current user:

``` bash
sudo chown -R $USER:$GROUPS ~/tmp
```

If that fails, we’d recommend either:

- Re-Installing Node.js with Bevry’s [recommended installation instructions](http://bevry.me/node/install)
- Asking about it on the [Node.js IRC Chat Room](http://webchat.freenode.net/?channels=node.js) (`#node.js` on freenode)


### When I run `npm install` on windows, I get `gyp ERR! configure error`
- For Windows XP/Vista/7 installations:
  - [Python](http://www.python.org/download/) [v2.7.3](http://www.python.org/download/releases/2.7.3#download) Recommended 
  - [Microsoft Visual Studio C++ 2010](http://go.microsoft.com/?linkid=9709949)
- For 64-bit builds of Node.js and native modules, you’ll also need:
  - [Windows 7 64-bit SDK](http://www.microsoft.com/en-us/download/details.aspx?id=8279)
    - If the install fails, try uninstalling any C++ 2010 x64&x86 Redistributable that you have installed first.
- If you get errors that the 64-bit compilers are not installed, you may also need:
  - [compiler update for the Windows SDK 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=4422)
- For Windows 7/8:
  - [Microsoft Visual Studio C++ 2012 for Windows Desktop](http://go.microsoft.com/?linkid=9816758)


### When I run `docpad run` on Windows, it asks me what program I would like to open the file in
It turns out that Windows will prefer to treat the local `docpad.js` file as the executable versus the global `docpad.cmd` file. To get around this, type `docpad.cmd run` instead in projects that have a `docpad.js` file. [More information here.](https://github.com/bevry/docpad/issues/561#issuecomment-21494426)


### Watching doesn’t work; works only some of the time; I get `EISDIR` errors
File watching is a pretty timid thing. We’re currently working on making it better. There are currently two methods for watching files: `watch` and `watchFile`. The default is `watch`, and it uses the operating system’s watching mechanisms. However, sometimes those mechanisms aren’t the best. If that’s the case, we’d like to switch our watching method to `watchFile`.  It’s slower, but it works when `watch` doesn’t. 

To do this, add the following to your [DocPad configuration file](/docpad/config):

``` coffee
watchOptions: preferredMethods: ['watchFile','watch']
```

Mac OS X users are most likely to encounter this issue.


### Watching is very slow to notice changes

Add the following to your [DocPad configuration file](/docpad/config):


``` coffee
regenerateDelay: 0
watchOptions: catchupDelay: 0
```

This will introduce problems however if you have previously customised `watchOptions`, or if your editor uses swapfiles. [More info here.](https://github.com/bevry/docpad/issues/749)


### Error: “We couldn’t find an existing DocPad project inside your current directory...”
This occurs when you run `docpad run` inside a directory that already has existing files, but doesn’t have a structure that resembles a DocPad project. We can’t directly ask you if you would like to use an existing [skeleton](/docpad/skeletons) for the basis of your new website, as pulling in a skeleton inside a non-empty directory may overwrite your existing files. If would like to still use a skeleton for the basis of your new website, you will have to run DocPad inside a new empty directory. If you would like to start your website from scratch (not use an existing skeleton) then you can follow the [Getting Started](/docpad/start) guide. Hope that helps :) [If you need more help then check out our Support Channels](/support).


### Error: “Could not locate git binary”
This happens when the [git](http://git-scm.com) installation is not exposed to your [`PATH` variable](http://en.wikipedia.org/wiki/PATH_%28variable%29). You can solve this in either of these two ways:

- Reinstall git and make sure to select the option during installation that asks if you would like to add it to your `PATH` variable (may also be called, would you like git to be available to the command line)
- Manually add the location your git binary resides in to your `PATH` variable

[More information about this here.](https://github.com/bevry/docpad/issues/425)


### Error: “EMFILE, too many open files”
As Node.js is like an octopus, able to do many things at the same time, sometimes Node.js will always try to do too many things than the operating system will let it. In which case, you can increase the amount of files allowed at the same time by running `ulimit -n 8192` in your terminal.


### How can I make DocPad go even faster?
There are a few things you can do:

- [Move files that you do not reference in content listings to a raw directory with the raw plugin](https://github.com/bevry/docpad/issues/276)
- [Set `standalone: true` to the meta data of documents that you regenerate often](/docpad/meta-data#standalone)
- Use native/JavaScript implementations of renderers instead of non-native, non-JavaScript ones
  - (e.g., instead of using SASS, use nodesass, Stylus, or Less)
- [Help us implement performance optimisations](https://github.com/bevry/docpad/issues/529)


### I upgraded, and it doesn’t work
[Check out the Upgrade Guides here](/docpad/upgrade)


### Whenever I output a variable (like `content`) it is escaped (`<` rendered as `&lt;`)?
Template engines by default _escape_ all variable output. Escaping is when we turn things like the open bracket `<` into its _html entity_ equivalent `&lt;`. This helps prevent malicious code accidentally being injected into your website which can open the door to XSS attacks. As such, we have to use a special syntax to keep the variable _unescaped_ when outputted. The special syntax is different for the templating engine your using, so here are the ways we know:

- Eco: `<%- content %>` instead of `<%= content %>`
- Jade: `!= content` instead of `= content`
- Haml: `!= content` instead of `= content`

### The output of a variable (like `document.title`) is empty or `null`
Be sure that you use the correct syntax for your template language, read the documentation of your chosen language.  
For example: When you want to put the output of a variable into the content of an (HTML) element in Jade, you must not write a whitespace between the element and the `=`. So this is wrong: `title = document.title` and that is correct: `title= document.title`


### I get a whole bunch of npm / missing module/package / installation failed errors
If you are using [Dropbox](http://j.mp/dropbox-bal) (an online syncing and backup tool) and your project is inside your Dropbox folder, then click the Dropbox menu icon and select “Pause Syncing”. 

Once that’s done, try whatever you were doing again. You may need to run `rm -Rf node_modules; npm install` as well. 

Once it’s all working, then you’re free to resume Dropbox syncing.

If you’re still experiencing issues, then be sure to post about it on the [issue tracker](/issues).


### The Growl notifications aren’t displaying
This means you need to [download and install the growlnotify extra](http://growl.cachefly.net/GrowlNotify-1.3.zip) from the [Growl website](http://growl.info). This package provides a command line application for calling Growl, which can then be used by DocPad.


### The exception raised by the Jade plug-in during documents generation makes no sense
The Jade compiler uses the full file content on the disk to show where the parsing error is. But since Docpad strips the meta header before submitting the data to the Jade compiler, you must add the number of lines of this header to get the right error spot in your code.


## Need more help?

- Found a bug? [File a Bug Report on the Issue Tracker](/issues)
- Need support? [Check out our Support Channels](/support)
