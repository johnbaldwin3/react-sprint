## Using the Import Keyword to Import Dependancies
We just finished up with how to install a build system using webpack from scratch. So this particular lesson about using import should be a good chance to catch our breath. We have been using the import statement throughout all of our React learning, so this should be a review mostly. The import keyword is a JavaScript keyword that allows us to bring in files, classes, function, other code, etc. into our document and use it whereever we need to.

### Using Imports

There are multiple ways of importing dependancies, for this particular lesson, let's look at a few of the main ones associated with dependancies.

1. import "default library name" from "library";
1. import "default library name", {"specific library module"} from "library";
1. import "another file";
1. import {"specific library module, another library module, and another module here"} from "library";

These are just the generic means in which we set up our imports, now let's look at the real usage of these below.

### Our imports
We just took a look at how to create the build system, and in doing so we can recall that we used npm to install and save our dependency libraries into our program. Import is the key that unlocks the door that they are installed behind and gives us access to them in our program. We won't go in depth about the install process since we just completed it, so let's take a look at our root JavaScript file: in this case we will call it 'app.js'.

Inside of any file that we plan to use a dependency in, we must import it. This goes for things like React, ReactDOM, React Router, jQuery, Underscore, Lodash, Backbone, etc. All of these extras must be imported into a file for us to use them. There are a few key parts to the import statement, so let's take a look at the set up and then define what is going on.

```js
//############# app.js ##################

//Third Party Library imports

//React Imports
import React, { Component } from 'react';
import ReactDOM from 'react-dom';

//React Router Imports
import {BrowserRouter, Route, Switch} from 'react-router-dom';

//Style Sheet import
import './styles/index.css';

```

This should not look entirely new, except for the use of React Router. But what is really going on?
At the beginning of our file we also have our import statements. These 3rd party library (dependency) imports must be installed above all other things inside of our file for the rest of our file to have access to them. So you will always see them at the top of the file.

In the first import, we see `import React, { Component } from 'react';`. What this means is that we are first importing React and all of the goodies that come with it. We could just leave it at that - and have access to everything we need, but we can save some time with by extracting specific portions of React into keywords that we will use in our application. `Component` for instance is something we use quite a bit of while building our, you guessed it, Components. By import the name Component, we can simply create a component like so:

```js
class MyComponent extends Component {
  //...
}
```

**Had we not imported Component by itself `{ Component }`:**
We would need to define our component as such:

```js
class MyComponent extends React.Component {
  //...
}
```

Either one of these works, but by including the brackets in our import we get access to `React.Component` by just using `Component` - handy, right?

We use ReactDOM to render our elements onto the DOM and that import statement should look very familiar. We simply use
`import ReactDOM from 'react-dom';` and then we are free to use it in our application under the name ReactDOM.

The next import - `import {BrowserRouter, Route, Switch} from 'react-router-dom;'` imports 3 different modules from our React Router Library. We then have access to call these Modules (Components in this case) in our app.js file. We will dive in to React Router soon, so we will explore those more fully when we open up that lesson.

Lastly, we import our style sheet. Very simply `import './styles/main.css'`. We do this because we of the way we designed our project to be bundled in our webpack set up. We can import directly to our root JavaScript file and it will all be bundled together (saving us from linking to it in our HTML).

### Conclusion
Importing our dependencies is a simple and straightforward process that we have been working with for a while now.
* Using the `import` keyword we are able to import files and dependencies in a variety of different ways.
* Importing gives us access to the libraries and it's modules inside of the file they have been imported.

#### References
* [MDN import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)
