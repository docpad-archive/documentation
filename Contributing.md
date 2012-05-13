So you've found a bug in DocPad or what to contribute a new feature? Great. Let's talk about the steps to get your patch into the official DocPad repository.

## 1. Forking and Cloning the Repository

When you go the [DocPad GitHub Page](https://github.com/bevry/docpad), there will be a "fork" button up the top right. Click that, it will set you up with your own "copy" of the repository, one that you can work on. Clone out your fork's url to your machine, and get working on it.


## 2. Configuring your Environment

Once you've cloned out your fork's repository, you'll need to configure your environment for working with DocPad. Here are the steps:

1. [Install Node.js](https://github.com/balupton/node/wiki/Installing-Node.js)

2. Install [Coffee-Script](http://coffeescript.org/) (which is what DocPad's source is written in)

    ``` bash
    npm install -g coffee-script
    ```

3. Install the project specific development dependencies

    ``` bash
    npm install
    ```

## 3. Writing Unit Tests

Our unit tests are written with [Mocha](http://visionmedia.github.com/mocha/) and can be found in the `test` directory. We use the [BDD](http://visionmedia.github.com/mocha/#bdd-interface) interface for writing our unit tests.

Use `npm test` to run our unit tests.


## 4. Submitting your Pull Request

Once you're all good, go back to the [DocPad GitHub Page](https://github.com/bevry/docpad) and click on the "Pull Request" button up the top right, and mention your changes.

Wait a while, and a project maintainer will get to your changes and pull them or provide suggestions what needs more work.

Cheers!