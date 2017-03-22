
## News

Official updates from the DocPad team:

- [DocPad Blog](https://blog.docpad.org)
- [Bevry's Blog](https://blog.bevry.me)
- [`#announcements` on the Bevry Slack](https://bevry.slack.com/messages/C099WE4UU/) - [Invite Link](https://slack.bevry.me)


## Trainings

Trainings covering DocPad. Oldest first.

- [DocPad Workshop at HasGeek 1/2](https://www.youtube.com/watch?v=Zu1uhI0uT2o) - March 2013
- [DocPad Workshop at HasGeek 2/2](https://www.youtube.com/watch?v=-LxKYZDeSsc) - March 2013
- [PluralSight: Build a Better Blog with a Static Site Generator](https://www.pluralsight.com/courses/static-site-generator-build-better-blog) - [Intro Video](https://www.youtube.com/watch?v=gHz9ZyxwcGQ) - March 2016


## Videos

Videos about DocPad. Oldest first.

- [Rapid Web Development with DocPad](https://www.youtube.com/watch?v=hvQCXDWh7Wg) - December 2012
- [Why DocPad Importers are HUGE!](https://www.youtube.com/watch?v=gEHXiZ4Wj4I) - July 2013
- [DocPad's Ecosystem](https://www.youtube.com/watch?v=5PxNY9w7Cj0) - September 2013
- [DocPad at Toronto Node.js Meetup](https://www.youtube.com/watch?v=i6dp_yqVCT0) - July 2013


## Skeletons

These skeletons are currently available to you as part of the DocPad bootstrap process:

<% unless @feedr?.feeds?.exchange?.skeletons?: %>
Something has gone wrong fetching the skeletons, please report this on [this GitHub issue](https://github.com/docpad/website/issues/70). Possible helpful data:

``` javascript
var exchangeUrl = "<%- @exchangeUrl %>"
var exchangeData = <%- JSON.stringify(@feedr?.feeds?.exchange, null, '  ') %>
```

[For the meantime, you can use this GitHub search.](https://github.com/search?q=topic%3Adocpad-project)

<% else: %>
<ul>
	<% for own skeletonID, skeletonValue of @feedr?.feeds?.exchange?.skeletons or {}: %>
	<li>
		<a href="<%= skeletonValue.repo.replace(/^git:/,'https:').replace(/\.git$/,'') %>"><%= skeletonValue.name %></a>
		- <code>branch: <%= skeletonValue.branch or 'master' %></code>
		- <%= skeletonValue.description %>
	</li>
	<% end %>
</ul>
<% end %>

Want to add yours? [Add it to the listing here.](https://github.com/docpad/extras/blob/docpad-6.x/exchange.cson)


## Posts

Community updates about DocPad. Oldest first.

- [DogFeet on DocPad](http://dogfeet.github.com/articles/2011/docpad.html) - Korean: Covers what is DocPad, getting started with DocPad, and customising DocPad
- [Dropbox auf dem eigenen Server](http://maxhaesslein.de/blog/1329055694) - German: Covers installing DropBox on both your local machine and your server's machine to easily sync your DocPad website
- [HTML UI on DocPad](http://htmlui.com/blog/2011-08-01-site-templates-with-static-html-nodejs.html) - Extensive writeup on their thoughts of docpad and how they are using it
- [Rebuilding JavaScriptQuiz.com with Node.js](http://www.aaron-powell.com/javascript/rebuilding-javascript-quiz-in-nodejs) - Covers their experience moving from Posterous to DocPad
- [JekyllのNode版であるDocpadを使ってみる](http://tomohisaoda.com/posts/2012/using_docpad.html) - Japanese: Covers getting started with DocPad and a comparison with other static site generators
- [Shop Talk Show Podcast](http://shoptalkshow.com/episodes/010-with-doug-neiner/) - A live web design and development podcast chat about the benefits of DocPad and <a href="http://code.dougneiner.com" rel="nofollow">Doug Neiner's</a> workflow (4 minutes in)
- [DocPad Talk @ Paris.js](http://djebbz.github.com/docpad-paris-js/) - Presentation of DocPad at Paris.js, May 30th 2012
- [Rapid Web Development with DocPad](https://vimeo.com/53755097) - DocPad founder Benjamin Lupton gives an overview of DocPad and showcases what building a site is like in it
- [Create professional websites with DocPad](http://emmet.io/blog/docpad/) - DocPad was an ideal solution for [Emmet documentation website](http://docs.emmet.io) because it not only provides a simplified development process, but allows me to reduce my hosting costs greatly
- [Why DocPad](http://takitapart.com/posts/why-docpad/) - Why I've built takitapart using a static site generator, and why DocPad won me over
- [Organising DocPad](http://takitapart.com/posts/organizing-docpad/) - Setting up the basic taxonomy of [takitapart.](http://takitapart.com)
- [WordPress → Aegea → DocPad](http://blog.sapegin.me/all/docpad) - It was much simpler than I thought and I like the result very much
- [Jekyll/Octopress to DocPad](http://blog.scriptybooks.com/from-jekyll-octopress-to-docpad/) - DocPad turned out to be the best platform for authoring interactive online technical books
- [Static Site Generation with Node.js and CoffeeScript](http://www.coffeescriptlove.com/2013/05/static-site-generation-with-nodejs-and.html) - DocPad embraces CoffeeScript in a big way
- [Converting to Docpad](http://fulljamesnet.herokuapp.com/articles/converting-to-docpad) - Web development worked perfectly
- [How to contribute to the Topcoat blog](http://vimeo.com/68060525) - Walks you through Adobe's workflow of using DocPad for the [Topcoat website](http://topcoat.io) and deploying to a GitHub Organisation Page
- [WordPress out, DocPad in](http://joefleming.net/posts/wordpress-out-docpad-in/) - Docpad looked super flexible for generating static sites, but it also allowed you to add dynamic pages to the mix. I couldn't be happier!
- [Multilingual blog on DocPad](http://blog.sapegin.me/all/multilingual-docpad) - How to make a multilingual blog with a single DocPad installation
- [blogger-docpad](https://github.com/dorajistyle/blogger-docpad) - Import Google Blooger articles by label and generate Docpad static blog. It's good example how to handle large number of files with docpad.
- [YTechie](http://www.ytechie.com/2013/11/blogging-awesomeness-with-a-static-generator-and-markdown/) - Blogging Awesomeness with a Static Generator and Markdown


## Websites

Websites built with DocPad. Alphabetically sorted. [Active listing](https://github.com/search?q=topic%3Adocpad-project). Historical listing:

- [Acherno Interior Design](http://acherno.com) - Corporate web site of the biggest interior design studio in Bulgaria
- [AlloyUI](http://alloyui.com) - [source](https://github.com/liferay/alloyui.com) - AlloyUI is a UI framework built on top of YUI3 that provides a simple API for building high scalable applications
- [Andrew Goodricke: Javascript Developer](http://andrewgoodricke.com/) - UK based Freelance JavaScript Web Application Developer with blog.
- [Artem Sapegin](http://blog.sapegin.me) - [source](https://github.com/sapegin/blog.sapegin.me) - Blog of Russian front-end developer: JavaScript, Stylus, Grunt.js, etc.
- [Bevry](http://bevry.me) - Creators of DocPad / Sydney based Node.js, JavaScript and HTML5 company focused on empowering developers.
- [Black Market](http://blackmarket.bg) - Bulgarian fashion company
- [CoApp](http://coapp.org) - [source](https://github.com/coapp/coapp.org) - CoApp is an open-source package management system for Windows
- [Cumulocity](https://cumulocity.com) - Internet of Things platform
- [DataTables Taglib](http://tduchateau.github.com/DataTables-taglib/) - [source](https://github.com/tduchateau/DataTables-taglib/tree/gh-pages) - Website of DataTables-taglib, a JSP taglib that allows to quickly create [DataTables](http://datatables.net) in Java/JEE based web application
- [DeLingua](http://www.delingua.si) - Slovenian translation company
- [DogFeet](http://dogfeet.github.com) - [source](https://github.com/dogfeet/dogfeet.docpad) - Korean: A development blog
- [Dorajistyle STATIC](http://dorajistyle.net) - Docpad generated Blog from Google Blogger articles.
- [Doug Neiner's Code Website](http://code.dougneiner.com) - [source](https://github.com/dcneiner/dougneiner.docpad) - Husband to one, father to three, jQuery Team Member, Senior Designer at [appendTo](http://appendto.com)
- [Emmet.io's Website](http://emmet.io) - [source](https://github.com/emmetio/emmet-docs/) - Emmet (previously known as Zen Coding) is a web-developer’s toolkit that can greatly improve your HTML & CSS workflow
- [Ferrari!=Ferrari](http://ferrari.github.io) - Chinese: A development blog
- [FizzVR](http://fizzvr.github.io/) - [source](https://github.com/fizzvr/vr-web) - Desarrollador web Backend Quito Ecuador
- [Florian's Blog](http://blog.boulay.eu) - [source](https://github.com/fboulay/website) - French: Technical blog on Java and technologies around the JVM
- [Game-Icons](http://game-icons.net) - Heaps of free SVG icons
welcome to my online portfolio
- [GreyCampus](http://www.greycampus.com/css-training-instructor-led) -The course offers complete information on Cascading Style Sheets (CSS) and teaches you how to control the look and feel of your HTML documents. This certification course also helps you in understanding the usage of fonts, colors, leading, and many other aspects.
- [HTML UI](http://htmlui.com/index.html) - Website all about frontend development
- [Imaginatr](http://www.imaginatr.com) - Imaginatr is a creative independent studio focused on the development of mobile applications and innovative software
- [Jose Quesada](http://josequesada.com) - [source](https://github.com/quesada/josequesada.docpad) - Homepage of Jose Quesada, a specialist with e-commerce database marketing
- [Kyle Pool](http://kylpo.com) - [source](https://github.com/kylpo/kylpo.com) - I'm in practice-mode: working hard for a successful life that improves the world.
- [Leigh Howells](http://leighhowells.com) - Home planet, blog and portfolio of Designer, tunesmith and UX Consultant, Cambridge, UK.  With added aliens.
- [The Mason Jar](http://www.the-mason-jar.com) - [source](https://github.com/the-mason-jar/www-the-mason-jar) - Hipster cocktails with a back-end powered by GitHub and DocPad.
- [MeltMedia](http://meltmedia.com) - An enterprise level web application development firm and interactive design agency based in Tempe, Arizona
- [MS Dev Show](http://msdevshow.com) - The MS Dev Show is the podcast for Microsoft developers covering news and topics such as Azure (cloud), Windows, and cross-platform development using MS tools.
- [Open Device Lab Hamburg](http://hamburg.opendevicelab.de) - Open Device Lab Hamburg. Come and test your Websites on a wide range of devices for free!
- [pimatic](http://www.pimatic.org) - smart home automation for the raspberry pi
- [Remy Bach](http://remy.bach.me.uk) - I'm a Christian, husband and father, front-end dev, gamer, and all around tech nerd!
- [Rob Rawkes](http://rawkes.com) - Rawkes is the home of Rob Hawkes, part-time Rawket Scientist and full-time geek. Join him as he explores the outer-reaches of programming, digital media, games, and everything in-between.
- [ShareLaTeX.com Blog](https://www.sharelatex.com/blog/) - Used to generate static pages for the blog
- [Surrey Vascular Surgeon](http://www.surreyvascularsurgeon.com) - Used to create a wesbite to explain vascular surgical services provided by me. Wanted a static website with fast load times.
- [takitapart.](http://takitapart.com) - akitapart. - pronounced "take-it-apart" - is the blog of Bob VanderClay, web application developer, founding partner at high90, and all around nerd
- [The Open Document Format](http://www.opendocumentformat.org) - The official website of the OpenOffice ODF file format
- [Tomohisa Oda](http://tomohisaoda.com) - Japanese: Web engineer and designer from Japan
- [Topcoat.io](http://topcoat.io) - CSS for clean and fast web apps by Adobe
- [The Open Document Format's Plugfest](http://www.odfplugfest.org) - The ODF plugfests are an ongoing series of vendor-neutral events, bringing together implementers and stakeholders of the standard
- [Vicktor Ilieff](http://www.viktorilieff.com) - Viktor Ilieff is an artist, conductor, composer and visionary. His art rests on the principle that the aesthetics of the means of expression should align with the times we live in.
- [v1rtual](http://v1rtual.net) - English & German: Blog about hacking, electronics, turtels and stuff
- [Notes From Heck](http://adityamukho.com) - Personal website and blog of Aditya Mukhopadhyay, built on the bootstrap skeleton.
- [YTechie](http://www.ytechie.com) - Blog for Jason Young, Azure Developer and Evangelist
