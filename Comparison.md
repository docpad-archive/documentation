This page will go into details about the differences between DocPad and other solutions like Rails, WordPress, Jekyll and Grunt.

## Rails (Web Development Framework)

Verdict: Overkill, Constraining

Rails is incredibly powerful and for the most part intuitive framework, perfect for streamlined systems. However the strong opinions and enforced conventions often lock you in to a particular way of doing things, which isn't always the best for your use case, and sometimes makes it incredibly painful to accomplish what you want when you have to stray from the standard way of doing things.

Data is stored in 3rd party database systems, which are incredibly powerful but have such huge burdens that they are more often or not left soley to the backend or databse programmers who is incredibly familar with the architecture and security threats, making agility quite difficult for the frontend programmers (or rather the team as a whole). Such burens include long learning curves, difficult and tiring installations on every machine running your project, migrations must be written to ensure your data does not get currupted between structure changes between machines, custom versional control implementations that aren't those we use everyday (GIT, SVN, CSV).

For simple websites such as blogs and other static websites, where we just need layouts and pre-processor support, rails is more than overkill, requiring the majority of time spent with burds like scaffolding, installations and route setups. It also makes it incredibly hard to move to another system when the static website grows up.


## Wordpress (<s>Content Management</s> Blogging System)

Verdict: Underkill, Constraining

Wordpress is king of the blog world, perhaps soley because it is king of the blog world.

Data is stored in 3rd party database systems, which are incredibly powerful but have such huge burdens that they are more often or not left soley to the backend or databse programmers who is incredibly familar with the architecture and security threats, making agility quite difficult for the frontend programmers (or rather the team as a whole). Such burens include long learning curves, difficult and tiring installations on every machine running your project, migrations must be written to ensure your data does not get currupted between structure changes between machines, custom versional control implementations that aren't those we use everyday (GIT, SVN, CSV).

Templates and layouts can only be used with the PHTML templating engine, and are only used as an asset to the Wordpress database which controls the routes, pages, and blog posts. The plugin system requires a long learning curve, and is incredibly basic and limited for such a popular system, making it very difficult if not inevitably impossible for programmers to extend the functionality.



## Jekyll (Static Site Generator)

Verdict: Underkill, Constraining

Jekyll is the most popular static site generator out right now, and it is exactly that. It generates a static website, and dies. It is not context aware, has poor support for different templating engines and pre-processors (which require implementation as hacks more than well written plugins), has no database that can be queryied to do custom listings of content (ruling out dynamic galleries, and anything besides simple blog rolls), and has no support for dynamic documents or custom routes that utilise its rendering abilities. For these reasons, it is more or less the Wordpress of the static site generator world.



## Grunt (Build System & Compiler)

Verdict: Powerful, Simplistic

Grunt (sames goes for Buildr, Brunch and CodeKit too) are build systems which are able to compile pre-processors, concantenate the result with other files, and finally minify them for web consuption. They can also be extended more or less infinitely to accomplish more functionality such as starting a simple web server, linting your files before compiling, and running unit tests. Which is fantastic for their use case of taking a bunch of files, and processing them with particular actions. Outside of these use case however, they ability platues as they only process documents rather than parse them leaving the naively unaware of the information their handling, making things such as complete static site generation impossible. Leaving them to be used only for their particular use case of build tasks.


## DocPad (Document Management System)

Verdict: Empowering, Liberating

DocPad on the other hand, takes a book from all of these systems. It provides the pre-processor and extensibility of build systems like grunt, the templating rendering and abilities of static site generators like Jekyll, and the power of web development frameworks like rails - without any of the bad bits.

It does this by parsing your website assets into an in memory database, with different directories for different purposes. The `documents` directory are files that are to be rendered, such as blog listings, markdown files, coffeescript files, etc. The `files` directory is for everything else. Layouts and partials also have their own directories.

Pre-precossors and template engines are provided by plugins, and are implemented in a similar way to the rails asset pipeline in that if you have the document `my-blog-post.html.md.eco` this will be rendering with the templating engine eco first to markdown, then with markdown to html. As such, we would write coffee-script files like `my-script.js.coffee`.

At compilation, DocPad renders all the documents and merges them with the files into an `out` directory. Unlike Jekyll, which just takes the source files, compiles them, and then regurgitates it all on top of the source files again - disgusting. Also unlike Jekyll, DocPad provides the templating engines with an in memory queryable database of everything we parsed, allowing you to do custom listings of documents, fetch in external data, and do all sorts of amazing things that using Jekyll are simply impossible.

Finally, as DocPad runs on Node.js, if you want more than generated static website, there is built in support for dynamic documents that will re-render on each request with the built in express server. You can even code in your own routes etc as well, or simply use DocPad as the rendering engine for your huge node.js web application. This is an awesome use case.

All in all, DocPad picks up all the benefits of the previous systems, and intergrates them together in a non-imposing, empowering, and liberating way.