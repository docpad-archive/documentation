```
title: "Intro"
```

<iframe width="640" height="360" src="http://www.youtube.com/embed/hvQCXDWh7Wg?list=PLYVl5EnzwqsQs0tBLO6ug6WbqAbrpVbNf" frameborder="0" allowfullscreen></iframe>

## What is DocPad?
DocPad is a next-generation web architecture. It allows **content management** via the file system, **rendering** via plugins, and **static site generation** for deployment anywhere. 

DocPad is built with Node and Express.js, making it fast and easily extensible.

## Problems with Traditional Web Architectures
Despite the wonders of current web application architectures, they’re mostly:

- **Inherently slow**
	- Usually built on live then die and blocking platforms
	- Performance is an afterthought, re-render every single time the default
- **Bloated**
	- Huge “include everything” code base; little or no code re-use (especially between frameworks)
	- Overkill for everything; no single project will use every feature of the CMS
- **Complex**
	- Gigantic learning curves, usually measured in months instead of days/hours
	- They require CMS/framework developers instead of web developers
- **Difficult**
	- Setting up a new website is time-consuming and complex
	- Uh oh! database not installed/version invalid
	- Migrations and deployments are a royal PITA
- **Limited**
	- WYSIWYG editors are sucky and stupid. Why reinvent the wheel? We’re already trained with (and love) our desktop counterparts: sublime, vim, word, byword
	- Abstractions on the go? Forget it. You're boxed in, unless you got a macheté
	- Want to use your own pre-processors, markups, and templating engines? Tough—that's handled by the core.


## DocPad, a Next-Generation Web Architecture
On the other hand, compare that with DocPad:

- **Inherently fast**
	- Built on a stay alive, non-blocking platform
	- Performance from the ground up; re-render only when changes occur, by default
- **Lightweight**
	- Built on a tiny core, with any reusable components abstracted into modules that other systems can use
	- Non-essential core functionality extracted into plugins, for opt-in functionality
- **Simple**
	- Tiny learning curve; get started in minutes, and pro within days
	- Web developers already have everything they need to get started
- **Easy**
	- Setting up a new website can be done in minutes
	- In-memory database allows querying without needing a manual installation
	- Migrations and deployments are handled via `git`, the tool we’re use to
- **Robust**
	- Use your desktop counterparts to edit content naturally: sublime, vim, word, byword
	- Abstraction-friendly; code the way you want, how you want
	- Use whatever language, pre-processor, markup, templating engine you want; it’s all covered by opt-in plugins

Furthermore, thanks to Node’s opt-in, modular philosophy, DocPad benefits from all the innovations of the Node community as a whole, including:
- [Socket.io](http://socket.io) for realtime communication between server and client
- [Browserify](https://github.com/substack/node-browserify) for sharing server code *directly* with the client
- Native pre-processor rendering such as [CoffeeScript](http://coffeescript.org), [CoffeeKup](http://coffeekup.org), [Stylus](http://learnboost.github.com/stylus), and [LessCSS](http://lesscss.org)

So, as the Node community grows and innovates, so too does DocPad. Awesome.



