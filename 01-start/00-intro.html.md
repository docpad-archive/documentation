```
title: "Intro"
```

<iframe width="640" height="360" src="http://www.youtube.com/embed/hvQCXDWh7Wg?list=PLYVl5EnzwqsQs0tBLO6ug6WbqAbrpVbNf" frameborder="0" allowfullscreen></iframe>

## What is DocPad?
DocPad is a next generation web architecture; allowing for content management via the file system, rendering via plugins, and static site generation for deployment anywhere. It's built with Node and Express.js, making it naturally fast and easily extendable.

## Problems with Traditional Web Architectures
Despite all the amazing wonder of current web application architectures, they're mostly:

- **Inherently slow**
	- Usually built on live then die and blocking platforms
	- Performance is an afterthought, re-render every single time the default
- **Bloated**
	- Huge include everything code base, little or no code re-use (especially between frameworks)
	- Overkill for everything, no single project will use every feature of the CMS
- **Complex**
	- Gigantic learning curves, usually measured in months instead of days/hours
	- You require CMS/framework developers instead of web developers
- **Difficult**
	- Setting up a new website is time consuming and complex
	- Uh ohh, database not installed or version invalid
	- Migrations and deployments are a royal pain in the ass
- **Limited**
	- WYSIWYG editors are sucky and stupid - why re-invent the wheel? We're already trained with and love our desktop counterparts (sublime, vim, word, byword)
	- Abstractions on the go? Forget it - you're boxed in, unless you got a machete
	- Want to use your own pre-processors, markups, and templating engines? Tough, that's handled by the core.


## DocPad, a Next Generation Web Architecture
On the other hand, let's compare that with DocPad, which is:

- **Inherently fast**
	- Built on a stay alive and non-blocking platform
	- Performance from the ground up, re-render only when changes occur the default
- **Lightweight**
	- Tiny core with anything re-usable abstracted out into a module other systems can use
	- Non essential core functionality moved into opt-in plugins
- **Simple**
	- Tiny learning curve - get started in minutes, and pro within days
	- Web developers already have everything they need to get started
- **Easy**
	- Setting up a new website can be done in minutes
	- In-memory database gives us querying without the need for a manual installation
	- Migrations and deployments are handled via git, the tool we're use to
- **Robust**
	- Use your desktop counterparts to edit content naturally (sublime, vim, word, byword)
	- Abstraction friendly - code the way you want, how you want
	- Use whatever language, pre-processor, markup, templating engine you want - it's all covered via our opt-in plugins

Besides this, thanks to the opt-in modular philosophy of node, we benefit from all the innovations of the community as a whole, including:
- [Socket.io](http://socket.io/) for realtime communication between the server and client side
- [Browserify](https://github.com/substack/node-browserify) for being able to share server-side code directly with the client-side
- Native pre-processor rendering such as [CoffeeScript](http://coffeescript.org/), [CoffeeKup](http://coffeekup.org/), [Stylus](http://learnboost.github.com/stylus/), and [LessCSS](http://lesscss.org/)

So as the node community grows and innovates, so do we. Awesome.


## Comparison Table

For those who like tables, here's the above in table form:

| Feature | Usual CMS (Drupal, Wordpress) | Usual Static Site Generator (Jekyll) | DocPad  |
|  ----- |  :-----: |  :-----: |  :-----: |
| Talent requirements  |  CMS developer  |  Backend+frontend developer  |  Frontend developer  |
| Developers proficient in  |  Months  |  Days  |  Days  |
| Plugin and extension system  |  Yes  |  No  |  [Yes](/docpad/extend) |
| Asset pipeline |  No  |  Implicit & bundled  |  [Explicit & extendable](/docpad/overview#the-documents-directory)  |
| Markup languages (markdown, rst, etc) |  No  |  1 bundled  |  Via [plugins](/docpad/plugins#renderers)  |
| Pre-processors (sass, less, etc)  |  No  |  No  |  Via [plugins](/docpad/plugins#renderers)  |
| Template engines (eco, jade, etc)  |  No  |  1 bundled  |  Via [plugins](/docpad/plugins#renderers)  |
| Database querying  |  Yes  |  No  |  Via [Query-Engine](https://github.com/bevry/query-engine/wiki/Using) |
| Layouts |  Yes  |  Yes  |  Yes  |
| Static website output |  No  |  Yes  |  Yes  |
| Re-render each request |  Yes  |  No  |  Via [`dynamic` field](/docpad/meta-data#dynamic)  |
| Extend the webserver  |  Yes  |  No  |  Via [events](/docpad/events#serverextend) and [API](/docpad/api)  |
| Watching  |  N/A  |  Yes  |  Yes  |
| Differential regenerations  |  N/A  |  No  |  Yes  |
| Live reload  |  No  |  No  |  Via [`livereload` plugin](/plugin/livereload/)  |
| Partials  |  No  |  No  |  Via [`partials` plugin](/plugin/partials/)  |
| Manual database installation required  |  Yes  |  No  |  No  |
| Import pages from file system  |  No  |  Yes  |  Yes   |
| Import pages from external database (mongodb, mysql, etc)  |  Yes  |  No  |  Via [plugins](/docpad/plugins#admin-interfaces)  |
| Import pages from external services (tumblr, dropbox, github, etc)  |  No  |  No  |  Via [plugins](/docpad/plugins#admin-interfaces)  |
| Import data from external services (atom, xml, json, etc)  |  No  |  No  |  Via [`feedr` plugin](/plugin/feedr/)  |
| WYSIWYG editors  |  Yes  |  No  |  Via [plugins](/docpad/plugins#admin-interfaces)  |



