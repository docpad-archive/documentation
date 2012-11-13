```
title: "Meta Data"
```

## Introduction

Meta data goes at the top of documents, and is defined by any character that repeats 3 or more times. For example, `---` is the most common usage, but you can also use `###` or whatever repeats 3 or more times. By default, we parse the meta data with [YAML](http://www.yaml.org/) but you can also use [CSON](https://github.com/bevry/cson) by doing `--- cson` instead.

An example document that uses meta data will look like this:

```
---
title: "Example Document"
layout: "default"
---

My example document content
```


## Special File Meta Data

### `title`
The title for the document. Useful for headings.

### `name`
Defaults to the `filename`. The name of the document. Useful for listings.

### `date`
Defaults to `mtime`. Useful for setting a custom date via your documents meta data.

### `slug`
Defaults to a slugified version of the `relativeBase`. Appears deprecated in favour of `url`.

### `url`
The url that you would like to use as the primary url for the document. When a user accesses a document via a secondary url, the user will be redirected to the primary url automatically.

### `urls`
Urls is the secondary urls for a document. It can be a comma seperated values list, or an array of values.

### `ignored`
Defaults to `false`. If set to `true`, the document will not be parsed. Useful for draft documents.

### `standalone`
Defaults to `false`. If set to `true`, when a change is detected for the document, we will only regenerate this document and not anything else (e.g. documents with `referencesOthers` set to `true`).


## Special Document Meta Data

### `referencesOthers`
Defaults to `false`. If set to `true`, this document will be regenerated when a change occurs in another document. It is automatically set to `true` whenever a template helper is called that references another document. This makes so for instance on a blog listing page, when a blog post is changed, we will also regenereate the listing as well as the blog post.

### `tags`
Defaults to `[]`. Tags can be a comma separated values list, or an array of values. While DocPad doesn't use tags for anything specifically, it is nice to have it handled uniformly across websites without you having to do it yourself.

### `dynamic`
Defaults to `false`. If set to `true`, the document will be re-rendered on each request. This also adds the `req` object to the template data - [req definition here](http://expressjs.com/api.html#request).


## Standard File Attributes

### `id`
The unique document indentifier. Defaults to the [cid](http://backbonejs.org/#Model-cid). When we get the `relativePath`, we set the id to that instead.

### `basename`
The file's name without the extension.

### `extension`
The file's last extension. E.g. will be set to `eco` for the file `hello.md.eco`.

### `outExtension`
The extension used for the output file. Same method as `extension` however it takes layouts into account as well.

### `extensions`
The file's extensions as an array. E.g. will be set to `["md","eco"]` for the file `hello.md.eco`.

### `filename`
The file's name with the extension.

### `path`
The full path of our source file.

### `outPath`
The full path of our output file.

### `dirPath`
The full directory path of our source file.

### `outDirPath`
The full directory path of our output file.

### `outFilename`
The file's name with the output extension.

### `relativePath`
The relative path of our source file.

### `relativeOutPath`
The relative path of our output file.

### `relativeDirPath`
The relative directory path of our source file.

### `relativeOutDirPath`
The relative directory path of our output file.

### `relativeBase`
The relative path of our source file without the file's extension.

### `contentType`
The MIME content-type for the source file.

### `outContentType`
The MIME content-type for the output file.

### `ctime`
The date object for when this file was created.

### `mtime`
The date object for when this file was modified.

### `encoding`
The encoding of the file.  Either `binary` or `utf8`.

### `source`
When `encoding` isnt `binary`, this is set to the raw contents of the file, stored as a string.

### `content`
When `encoding` isnt `binary`, this is set to the  contents of the file, stored as a string. The different with this and `source` is that trailing whitespace is removed as well as the tab character is converted to 4 spaces.


## Standard Document Attributes

### `header`
The file meta data (header) in String format before it has been parsed.

### `parser`
Defaults to `yaml`. The parser we used to parse the document's meta data header.

### `body`
The file content (without the meta data header) before we've rendered it.

### `rendered`
Defaults to `false`. Set to `true` once we have been rendered.

### `contentRendered`
The rendered content (after is has been wrapped in the layouts).

### `contentReneredWithoutLayouts`
The rendered content (nenfore being wrapped by the layouts).
