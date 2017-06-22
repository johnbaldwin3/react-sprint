## Using Webpack To Make Your Own Build System
We examined the reasons why we would want to use build systems to help our workflow in web development, but we did not really get into how to incorporate them into our projects. We know that `create-react-app` does a lot of this heavy lifting for us, but let's take a step back and learn how to create our own build system using npm, Node.js, Babel, along with webpack. Webpack has surfaced as a go to build system for React developers.

### Getting Started with Webpack
Webpack is one of our "doer" build systems. Webpack was built with an understanding that the vast majority of JavaScript based application require the same dependencies. With that in mind, it comes built with a standard array of tools to help most apps, and yet remains flexible to being customized for each project. It will ease our burden and help us perform tasks to make our application production a lot more streamlined. The benefits of using webpack circle around 3 main things.

1. Loading modules
1. Minifying code
1. Concatenation

Let's examine each of these in more detail and then begin to piece our project together from the beginning.

#### Loading Modules
Webpack uses module loading to read the source files of our application and search for the dependencies needed to create our application. This modular set up helps the efficiency of the application and prevents likely errors by making sure our project has what it needs to work.

#### Minification of code
You probably know by now that when you code, you can author some very large documents with many lines of code involved. This wreaks havoc on the efficiency of the program. The way around that issue is called minification. It's a crazy word that simply means to compact the file into the very basic needs without any filler, such as spaces or unnecessary characters within our code. For example if we had a variable in one of our files `var mySuperLongVariableName = "some stuff here"`, webpack would then use a minifying process to compact our code into something that might simply be `var a="some stuff here"` - essentially removing all of the fluff from our coding and making a condensed compact copy of that file.

#### Concatenation of Files
The last major role of webpack is to concatenate our files. Webpack searches through our source code and combines files into one file so that we don't have to load multiple pages for our application to work. Often this file is called "bundle.js" that represents a bundle of our files that have been modularized and minified as well.

### Getting started
So how do we get a project going with webpack? The first step we need to do is go into terminal and use bash to create a new directory for our project. This can be named whatever you wish.

```
$ mkdir my-new-app
```

We then need to change into that directory.

```
$ cd my-new-app
```

The next step is to initiate a project with dependencies. This will give us a platform (in the form of a Node.js package) to start building our build system with some default goodies baked in. Inside of our project directory we will initialize a generator that automatically detects an keeps track of the dependencies and devDependencies that are added as we go along.

```
$ npm init -y
```

The file that is created is called `package.json`. We will examine it a bit more down the road, but the important take away is that we have created that file within our directory.

### The install series...
We are going to now install some dependencies and devDependencies using npm and we will discuss what they are as we do so.

#### Install React and other libraries of your choosing.
This is a customizable step, and depends on which portion of the React stack that you wish to work with. For this particular build system, let's install React and React Router.
So inside of our project folder in terminal we are going to use bash to run an npm install.

```
npm install --save react react-dom react-router-dom
```

The command we gave terminal tells the computer that we want to install and save inside of our project folder (`--save`) the libraries of `react`, `react-dom`, and `react-router-dom`. This will automatically fetch the most recent versions of these libraries and install them in our project so that we can import them whenever we need them in our source code files.

#### Install webpack as a devDependancy.
Next, we are going to install webpack. Webpack is a devDependancy so we will install it in a similar but not identical fashion as we did with the React stack.

```
npm install --save-dev webpack
```

The major difference here is that we add the `-dev` after the `--save` command. This lets our package.json file know that we are installing this item as a devDependancy.

#### The transpilers
Let's keep moving along and install our transpilers. When we transpile, we go from one language to another such as "JSX -> JavaScript". For this step we are going to use Babel. Babel is another "doer" tool in our build system. Babel's main focus is translation. It has tools to take our JSX language we use in React and change it into regular JavaScript that the browser is able to interpret. We also are going to depend on Babel to transpile our ES2015 JavaScript syntax into the ES5 syntax which has more widespread support from all browers. This install involves two pieces: Babel Core and Babel Loader. Babel Core is the heart of the Babel build system and revolves around all of the transpiling. The Babel Loader is a plugin that allows us to install preset configurations into Babel to transpile specific code.

We can install all of this using npm again, so in terminal inside of our project folder:

```
npm install --save-dev babel-core babel-loader
```

Babel is a modular build system that is split between between plugins and presets. After we have added these to our devDependencies we need to add the pieces of the plugin so that we can instruct our application on which specific sets of Babel transpilers (called "presets") to include. To do this we go back to our project directory in terminal and put npm back to work.

```
npm install --save-dev babel-preset-react babel-preset-es2015
```

This has now installed the presets to give Babel the power to transpile React (JSX) `babel-preset-react` to regular JavaScript, and also to transpile `babel-preset-es2015` ES2015 (ES6) syntax to ES5 syntax.

Now we should be able to open up our project using our code editor.. if you are using Atom, then you can simply type `atom .` using bash in terminal inside of the project directory. What you should see is the beginnings of a project with a package.json file inside of the folder.

To get our Babel transpiler up and running we will need to create a new file to configure the way we plan to use Babel. You can do this in your terminal using `touch .babelrc` or you can simply right click on the folder inside of atom and select create new file. The config file should be named ".babelrc". The leading period before the file name signals that this file should remain hidden.

#### .babelrc
After creating our ".babelrc" file, let's open that file up inside of Atom. It should be completely blank.

Inside of our .babelrc file, we need to create an object containing our presets that we installed with npm.

```js
//########## .babelrc ############
{
  "presets": { "es2015", "react" }
}
```

These simple lines of code let's Babel know which presets to include and use in our application when transpiling our source code.

#### webpack.config.js
We now need to create a configuration file for our webpack build system. To do this, we first must create a new file. You can use the `touch` method to create this file or directly create it inside of Atom as well. We will need to create a file called "webpack.config.js" inside of our project folder.

After we create this file, we will need to open it up and set up the configuration of our webpack build system.

Inside of webpack.config.js we will type the following and explain afterwards exactly what we did.

```js
//########## webpack.config.js ############
module.exports = {
  entry: './app.js',
  output: {
    filename: 'bundle.js'
  },
  module: {
    loaders: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        loaders: ['babel-loader']
      },

    ]
  }
};
```

The first part of our webpack config file is an export statement, which allows us to export the rest of the information to another file for us to use in our project - we do this by using `module.exports = {}`. We'll come back to that in a second.

Inside of the object that we export, we have three main sections:

1. entry:
  * The entry property takes a value of a string, which is specifies a path name to the file that will act as the index/root JavaScript file for our entire application. Meaning all of our JavaScript will need to import into this file. In this case we have named it "app.js".
2. output:
  * The output property takes an object as it's value with a key "filename" and that gets the value of the concatenated JavaScript files. This is commonly named "bundle.js". This is where our code is transported to, and run during production.
  * We are also able to give the output property a `path: ""` property that takes a string which would designate where the bundle.js should be stored. This is commonly a "build" or "dist" folder.
  * We can now go create a singular script tag in the bottom of our html file just above the closing body tag -- just be sure that the pathname matches the location of the actual bundle.js file.

  ```html
  <body>
    <script src="bundle.js" />
  </body>
  ```

3. module:
  * The module property has a value of "loaders". The loaders are what we use to determine which plugins we want to run. The module object generally consists of a propert called "loaders" that is made up of an array of objects that determine which plugins/loaders should be used. The a loader object generally consists of three properties.
    1. test:
      * The test property takes a regular expression as a value and is used to determine which file extensions need to be translated.
    2. exclude:
      * Exclude takes regular expression with a folder name and excludes any files within that folder from being run against the loaders. This is almost always our "node_modules" folder where our libraries and dependancies are stored.
    3. loader(s):
      * The loader or loader property takes an array of loader plugins, such as "babel-loader". If using more than one loader becomes loaders.
      * In our example we will rewrite a few of our webpack settings as we move through, so we will change our loader to loaders for example.

### Time to build
We are essentially set up for a very bare bones webpack build system, a few more steps and we could get up and running with a minimal application.
The next step of the process is to go ahead and build the structure of our application. We could do this one of two ways. If we had opted to install webpack globally on our computer we could simply go into terminal and type webpack. We did not build out that way, so we must use option two.

Inside of terminal in our project directory we are going to run the following command:

```
node_modules/.bin/webpack
```

This command will do a one time run through of our project and sort through the webpack settings we have created and create the bundle.js file we need to get going in our project.

This is not really an ideal way to update our application any time we make changes, so we will create a script in our package.json file that will automate this process for us.

Inside of our package.json file under the scripts property we need to add a build script:

```json
######## package.json ########

"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack",
  },
```

The syntax must match exactly as you see here since it is a JSON object.

This build script prevents us from having to type out the `node_modules/.bin/webpack` command over and over to update our app. It is now set to automatically do so.

#### Development Server
So we kind of began the process of automating our applications build process - but we can go even further in assisting our cause. We can add a "dev server" or development server to our project. The dev server is designed to prevent us from, constantly having to reload/refresh our browser window. This means we can track our changes in our saved document as we proceed along in developing it.

The first step is to install the webpack-dev-server.

```
npm install --save-dev webpack-dev-server
```

Now that we have installed it, let's put it to use inside of our package.json file. Underneath our build script, let's add a start script.

```json
######## package.json ########

"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack",
    "start": "webpack-dev-server",
  },
```

This allows for us to start up a local host server which will display our project for us and update it whenever we make changes and save our project. In terminal in our project directory, we can simply run the following code:

```
npm start
```

Assuming all things are installed correctly, this should start your development server up. If you need access to another terminal window you can use `command + t`, and if you wish to stop your development server you need to use the `ctrl+c` keys together (control and c keys). Now in your browser, you can type `localhost:8080` which is the default port for your local host server. We can change the port to whatever we wish by adding a port in our start script. For instance if we wanted to change our port to 3000, we would go to our package.json file and add the following: `--port 3000` as demonstrated below.

```json
######## package.json ########

"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack",
    "start": "webpack-dev-server --port 3000",
  },
```

Any additions will require you to stop your dev server and restart it by going into terminal and first using `Ctrl + C` (control and c) to stop the server then `npm start` to get it running again with the new changes.

There are a few other helpful tools we want to add on top of this to make our build system with webpack even better.

#### Progress indicator
Inside of our package.json let's add another tool to track our progress during the building of our app and build system itself. By adding `--progress` in our start script we can monitor the progress indicator during the build.

```json
######## package.json ########

"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack",
    "start": "webpack-dev-server --port 3000 --progress",
  },
```

#### CSS and Style Loaders
The same way that we set up our app to track changes to our JavaScript, we can do with our styling pages too. First we need to install two tools "style-loader" and "css-loader". To do that we go into our terminal project folder and type the following:

```
npm install --save-dev style-loader css-loader
```

After we have installed these devDependancies, we need to go back into our webpack.config.js file and update our module to be able to use these.

```js
//########### webpack.config.js #########

module.exports = {
  entry: './app.js',
  output: {
    filename: 'bundle.js'
  },
  module: {
    loaders: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        loader: ['babel-loader']
      },
      {
        test: /\.css$/,
        loader: 'style-loader!css-loader'
      }

    ]
  }
};
```

We have added another object after our first set of loaders, this time with a test to check for css files and then the loaders.
We add the loaders in the order we want them to run, in this case, we want our style sheets loaded together before the css is loaded. We chain these two loaders together by using a `!` exclamation mark in between them. This means that we can now import our stylesheet directly into our root JavaScript directory as we would any other import statement with a path and filename. It will now be scooped up in the bundle of things and we don't need to worry about it.
**This also means we can delete any links to our css inside of our index.html page.**

#### inline -- all file changes updated
Now that we are using our CSS in the dev server, lets make sure we are updating everything in real time across all of our files. To do this, we add `--inline` to our start script in the package.json file.

```json
######## package.json ########

"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack",
    "start": "webpack-dev-server --port 3000 --progress --inline",
  },
```
Inline really is geared toward styling and will let us update with every save of our project as we move along in real time on the dev server.

##### The final problem, how are you gonna react to this?
There remains one slight issue with our set up, and it all has to do with the way React works using State. When developing a React application we need to constantly test our components to make sure we handle the state of the program correctly and that the components are rendering and responding as they should. The problem with our current set up is that each time we refresh the page after making changes to something like a background color... we lose our state. So if for instanced we had a component that we had entered 10 items into as a list, each time we rendered we would have lost that data and would be required to type it back in manually.

Have no fear though my friends, we can get through this together. We need to add an option called hot-loading. More specifically `react-hot-loader`. To do this we first start out in terminal inside of our project directory.

```
npm install --save-dev react-hot-loader
```

Now, you might be able to guess our next stop: webpack.config.js, where we need to update our loaders. We also will need to change our "loader" to **"loaders"** inside of our module (see below). This is a JavaScript based loader so we can add it next to our Babel-loader like so:

```js
//########### webpack.config.js #########

module.exports = {
  entry: './app.js',
  output: {
    filename: 'bundle.js'
  },
  module: {
    loaders: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        loaders: ['react-hot-loader', 'babel-loader']
      },
      {
        test: /\.css$/,
        loader: 'style-loader!css-loader'
      }

    ]
  }
};
```

We are almost done, but we first need to enable this inside of our start script using `--hot`:

```json
######## package.json ########

"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack",
    "start": "webpack-dev-server --port 3000 --progress --inline --hot",
  },
```

One final detail to point out is that hot-loading relies on a singular entry file (like app.js or index.js). All of our other components should be imported into this file in order for our hot-loading to work. If we were to use components directly inside of this file, each change we made would effect state. This is why we commonly create a file tree system, with a folder dedicated to our components, models, etc.

### Conclusion
Webpack is a powerful tool to help our programming game. We have walked through the entire process fairly thoroughly, but this probably will take a few reviews to fully get the hang of. The good news is that we have tools like create-react-app and yeoman generators to take care of this for us most of the time, and now you hopefully you are able to understand what is beneath hood of our build systems.

#### References
* [Webpack](https://webpack.github.io/)
* [Babel.js](https://babeljs.io/)
