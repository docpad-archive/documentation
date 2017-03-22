---
title: Performance Optimizations
---

This section still needs a lot of work, but it can be a good start. :)

## Using the [raw](https://github.com/docpad/docpad-plugin-raw) plugin

**Note:** We now recommend using the `copy` plugin, which is an improved version
of the `raw` plugin. <https://github.com/almero-digital-marketing/docpad-plugin-copy>

This plugin allows you to quickly copy files that are found in the `/src/raw`
directory to the `/out` directory without going through DocPad's rendering, thus
making it a much quicker process.

Especially useful if placing them in the `/src/static` (or `/src/files`)
folder is still slow.

Check the [plugins section of the DocPad docs](https://docpad.org/docs/plugins) for instructions
on how to install plugins.
