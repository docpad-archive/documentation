So you've found a bug in DocPad or what to contribute a new feature? Great. Let's talk about the steps to get your patch into the official DocPad repository.


## 1. Fork and Clone the Repository
When you go the [DocPad GitHub Page](https://github.com/bevry/docpad), there will be a "fork" button up the top right. Click that, it will set you up with your own "copy" of the repository, one that you can work on. Clone out your fork's url to your machine, and get working on it.


## 2. Prepare your Environment
Once you've cloned out your fork's repository, you'll need to setup your clone for development. To do this, run the following inside your clone's directory:

``` bash
make clean
make dev
```

This will install all dependencies that we need for development, as well as start watching our source [CoffeeScript](http://coffeescript.org/) files for changes and re-compile them when a change is made. You'll probably want to open a new tab (or console window) to perform your git commands while the CoffeeScript watcher runs in that window.


## 3. Write Tests
Our tests are written with [Joe](https://github.com/bevry/joe/) and can be found in the `src/test` directory. Use `npm test` to run the tests.


## 4. Submit your Pull Request
Once you're all good, go back to the [DocPad GitHub Page](https://github.com/bevry/docpad) and click on the "Pull Request" button up the top right, and mention your changes.

Wait a while, and a project maintainer will get to your changes and pull them or provide suggestions what needs more work.