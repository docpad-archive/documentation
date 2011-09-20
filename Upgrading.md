## Upgrading from 0.x to 1.0

1. Install docpad with the new global dependences `npm -g install coffee-script commander cson docpad`
2. Any of your `documents` or `layouts` which use the eco templating engine should have the extension `.eco` appended. E.g. `layouts/default.html` to `layouts/default.html.eco`.
3. Any of your `documents` or `layouts` which utilise a markup language should have the extension `.html` prepended. E.g. `documents/something-in-markdown.md` to `documents/something-in-markdown.md.html`
4. These changes allow for some new incredibly powerful possibilities, such as allowing other templating engines other than eco, and allowing for multiple and more explicit markups to be applied to the files.