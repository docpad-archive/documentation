## Rendering

```
document.pdf.md.eco
> pdf.render(md.render(eco.render(document)))

document.pdf.html.md.eco
> pdfFromEco(htmlFromMd(mdFromEco(document)))

document.md extends layout.html
> html.render(layout, md.render(document))

document.md
> md.render(document)
```