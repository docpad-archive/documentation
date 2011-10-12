(work in progress)
## Installation using the native binary ##

This guide will describe how to set up docpad to work under windows using the native nodejs binary (v0.5.9 as of writing). I assume in this you want to have nodejs in C:\node and your packages in C:\node\packages. Change if you like it differently.

1. Download the latest nodejs.exe from [nodejs.org](http://nodejs.org).
2. Put it in C:\node, make a new folder C:\node\packages.
3. Add C:\node to your system path and create a new variable called NODE_PATH, using C:\node\packages as value.
4. Before you start installing docpad, lets set up coffee-script. Download the latest version from [here](https://github.com/jashkenas/coffee-script) and unzip it to the \packages folder, name it "coffee-script".
5. We want a system wide coffee executable, best is to follow the "Better solution" hint at the bottom of [this page](https://github.com/alisey/CoffeeScript-Compiler-for-Windows). To verify it works, open the console and type "coffee --help". If you see the usual output, you're fine.
6. Download docpad and extract it to the \packages folder. you can try to start it by opening the console, changing directory to the ...\docpad\bin folder and running "coffee docpad". You will see errors. To fix these you have to install the missing packages. That's where the nasty part starts.
7. To install packages you have to do the work that otherwise npm did for you:
    1. Download the package you want from the [npm repository](http://search.npmjs.org/)
    2. Extract it to the packages folder
8. You'll be busy for a while. But if you satisfy all dependencies, you should be fine.

## Pitfalls  ##
There are some pitfalls you have to workaround.

* There is a line where commander.js get's required from an uncommon origin (using node_packages). Either move commander or change the path in the code.  
* In my case, coffeekup couldn't be found because the library was sitting in .../coffeekup/src and not .../coffeekup/lib - cleanest solution is to place a index.js in .../coffeekup, exporting the script in src.  
* When it first seems to work, you will notice that some plugins didn't get loaded properly - sadly, the warnings obscure the actual problem that modules are missing. To find these out, simply run the plugin script in question with the coffee command to be able to debug them.  
* I have not tested this on a fresh windows install - I have some gnu tools from gnuwin32 in my path as well as the tools from mysysgit, this might have had inpact on the (positive) function of some modules? Just a guess.