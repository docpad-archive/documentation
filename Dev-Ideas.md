## Rendering

```
document.pdf.md.eco
> pdf.render(md.render(eco.render(document)))
> document.pdf

document.pdf.html.md.eco
> pdf.render(html.render(md.render(eco.render(document))))
> document.pdf

document.pdf.html.md.eco
> pdfFromEco(htmlFromMd(mdFromEco(document)))
> document.pdf

document.md extends layout.html.eco
> html.render(eco.render(layout, md.render(document)))
> document.html

document.md
> md.render(document)
> document.md (as html)

document.md
> document.md (as md)

document.html.md
> htmlFromMd.render(document)
> document.html (as html)
```

``` coffeescript
markdownRenderer = class extends BaseRenderer
  supportedExtensionCombinations: [
    {in:/^md|markdown$/, out: /^html$/}
  ]
  render: (inExtension, outExtension, content) ->
    markdown.render content

jadeRenderer = class extends BaseRenderer
  supportedExtensionCombinations: [
    {in:/^jade$/, out: /^xml|x?html$/}
  ]
  render: (inExtension, outExtension, content) ->
    jade.render content

ecoRenderer = class extends BaseRenderer
  supportedExtensionCombinations: [
    {in:/^.*$/, out: /^.*$/}
  ]
  render: (inExtension, outExtension, content) ->
    eco.render content

coffeeRenderer = class extends BaseRenderer
  supportedExtensionCombinations: [
    {in:/^coffee$/, out: /^js$/}
    {in:/^js$/, out: /^coffee$/}
  ]
  render: (inExtension, outExtension, content) ->
    if inExtension is 'coffee' and outExtension is 'js'
      coffee2js.render content
    if inExtension is 'js' and outExtension is 'coffee'
      js2coffee.render content
```