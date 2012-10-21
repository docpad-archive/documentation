# Debugging Docpad

Sometimes shit just does bad and you need to get into Docpad and work out what's happening. A plugin may be not working as expected, content isn't being generated or you're just curious as to how to do it. Well for that you'll need to get your debugging on.

*Note: I've only tested the following under OSX but Docpad and node-inspector both work under Windows from what I understand*

## What you'll need

* [node-inspector](https://github.com/dannycoates/node-inspector)
* A webkit based browser (you know, like Chrome :P)

## Debugging coffee-script

Since `CoffeeScript` (which Docpad is written in) actually compiles to JavaScript it can be a bit tricky to debug. Check out the [install guide](http://coffeescript.org/#installation) for CoffeeScript as it covers how to get it to run in debug mode.

For the click impaired you need to append `--nodejs --debug-brk` to get a good debugging experience.

# Firing up Docpad in a debugger

Once you've installed [node-inspector](https://github.com/dannycoates/node-inspector) and got it running in the background (running it in the background is much easier) you can start docpad with the following command:

    ./node_modules/.bin/coffee --nodejs --debug-brk ./node_modules/.bin/docpad run

1. I assumed CoffeeScript and Docpad are installed locally not globally with `npm`
2. You can use any of the docpad commandline switches

## Understanding --debug vs --debug-brk

As a side note there are two ways to debug a nodejs program you can use `--debug` or `--debug-brk`. The primary difference is how the first breakpoint is found. When using `--debug-brk` you will be *stopped on the first line of the application* whereas `--debug` will just allow you to use breakpoints.

The other difference I've found is that if you don't use `--debug-brk` then node-inspector wont be able to hook into the [debugger](https://developer.mozilla.org/en/JavaScript/Reference/Statements/debugger) keyword.

If you're wanting to either step into the running Docpad instance as it starts up **or** use the `debugger` keyword then you'll need to use `--debug-brk`.

# Debugging the CoffeeScript

Since CoffeeScript isn't really a language that nodejs uses it can be a bit trickier to step into. If you know the exact place you want to breakpoint **use the `debugger` statement**. This will save you a lot of time trying to get to the right line.

If you don't know the line you will need to step into each command as its executed, especially the `require(./foo.coffee')` commands. Be warned, that can be really time consuming as you have to go deep through nodejs before it will give you a file that is the generated CoffeeScript output.

The third kind of debugging you may want to do is the debugging of Docpad once it's running (say you want to see how a request is handled, what happens during regeneration of the site, etc). This can be made easier with the `debugger` command but it is also doable from just the node-inspector UI. Once you have Docpad running you'll need to refresh node-inspector, doing so will then populate the `scripts` tab with **all** JavaScript files load, **including those output from CoffeeScript**. The files which CoffeeScript has generated will be with a `.coffee` extension, you can open them up and see the generated JavaScript and put your breakpoints in.