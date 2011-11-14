## HELP!


### I upgraded, and it doesn't work

[Check out the Upgrade Guides here](https://github.com/balupton/docpad/wiki/Upgrading)


### Whenever I output a variable (like `content`) it is escaped (`<` rendered as `&lt;`)?

Template engines by default _escape_ all variable output. Escaping is when we turn things like the open bracket `<` into it's _html entity_ equivalent `&lt;`. This helps prevent malicious code accidentally being injected into your website which can open the door to XSS attacks. As such, we have to use a special syntax to keep the variable _unescaped_ when outputted. The special syntax is different for the templating engine your using, so here are the ways we know:

- Eco: `<%- content %>` instead of `<%= content %>`
- Jade: `!{content}` instead of `#{content}`
- HAML: `!= content` instead of `= content`


### I get the error: `Cannot find module 'buildr'`

Run `npm install buildr` and that'll fix it. This is because the skeleton you're currently running utilises the buildr plugin, as such we need to have buildr installed.


### I get CoffeeScript errors

Try installing the latest version of CoffeeScript via `npm install -g coffee-script`. Versions 1.1.1, and 1.1.3 and up are supported. If you still get problems, post them in the [issue tracker](https://github.com/balupton/docpad/issues).


### I get a whole bunch of permission denied errors

DocPad handles the installation of the npm modules of it's plugins automagically, as such it needs write access to it's own directory (usually `/usr/local/lib/node_modules/docpad`). If you didn't follow the [recommended installation instructions](https://github.com/balupton/node/wiki/Installing-Node.js), you can try running `sudo chown -R $USER /usr/local` to rectify the permission problems. Alternatively, you can run docpad under sudo, but that probably isn't the best solution. If all fails, uninstall node, and re-install it using the [recommended installation instructions](https://github.com/balupton/node/wiki/Installing-Node.js).


### I get a whole bunch of npm / missing module/package / installation failed errors

If your using [DropBox](http://db.tt/RxyNWZw) (an online syncing & backup tool) and your project is inside your DropBox folder, then click the dropbox menu icon and select "Pause Syncing". Once this is done, try whatever you were doing again, you may need to run `rm -Rf node_modules; npm install` as well. Once it's all working, then you're free to resume dropbox syncing.

If you're still experiencing issues, then be sure to post about it on the [issue tracker](https://github.com/balupton/docpad/issues).


### The growl notifications aren't displaying?

I got confused by this too, turns out you need to [download and install the growlnotify extra](http://growl.cachefly.net/GrowlNotify-1.3.zip) from the [growl website](http://growl.info/). What this package does it provides command line applications the ability to call growl which is needed as docpad is a command line application.

### The exception raised by the jade plug-in during documents generation makes no sense.

The jade compiler uses the full file content on the disk to show where the parsing error is. But since Docpad strips the meta header before submitting the data to the jade compiler, you must add the number of lines of this header to get the right error spot in your code.