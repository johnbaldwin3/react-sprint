## Exporting Classes and Functions in JavaScript
We just finished looking at how to import our third party libraries, dependencies, and singular files. Let's look at the other side of the spectrum and how we can export important things, such as classes and functions, in our JavaScript files - and also how we can import those various things back in to another file. Exporting allows to use and reuse bits of code over and over again throughout our entire program without having to rewrite the code over and over again.

### Exporting functions - as a default
There are two basic means to export anything in JavaScript. Let's start at the most simple level and export *one* default function from within a file and then import it into another file to use it. When using the `default` keyword (which you will see below), we can only export one item from the file. This one item is the default - and essentially stands for everything that file represents.

Let's look inside of a file called "function.js". We are going to create a super complex function that will take in one argument and return a string using that argument. It's important to note that we can export this function in a variety of ways, even using default, so we will take a look at the options as well.

Case #1:

```js
//########### function.js ###########

//the simplest means is to create an inline export statement:
export default function myFunction(name) {
  console.log("Hello, my name is " + name);
  return name;
}
```

We can then go inside of another file and import that function using an `import` statement. Let's pretend we needed to use that function inside of our "index.js" file for some reason. We are simply going to point our import statement to the pathname for our function.js file (these are in the same folder in this example).

```js
//########### index.js ##############

//we can leave off ".js" file extensions in JavaScript
import myFunction from './function';

//we can now use our function with the name myFunction because of our default export statement.
myFunction("Hans Solo");
//output in console = "Hello, my name is Hans Solo"
```

This works very simply, but below let's look at how we could do the exact same thing, just a bit differently:

Case #2:

```js
//########### function.js ###########

//we export defaults at the bottom of our page too...
function myFunction(name) {
  console.log("Hello, my name is " + name);
  return name;

export default myFunction;
}
```

This method above would let us import the same exact way. There is no functional difference between the two.

### Exporting Functions - multiple or modular
To review, using default is reserved essentially for just one thing being exported from a file. The case changes when we need to export multiple items from a file, as we are not allowed more than one default. The good news again is that we have seen this before.

For this example, let's go back to our "function.js" file and add another function to our file - we will then export both functions and import both function back into our "index.js" file. We will look at a couple ways in which we can achieve the same results.

Case #1: (multiple files, multiple exports)


```js
//########### function.js ###########

//we can export each function inline.
export function myFunction(name) {
  console.log("Hello, my name is " + name);
  return name;
}

export function anotherFunction(day) {
  console.log("Today is " + day);
  return day;
}

```

We simply add export before each of our function declarations. Now to use those functions in our "index.js" file, let's import them both as modules from our file like so:

```js
//########### index.js ##############

//we use { } to group the items we wish to import from the file.
import { myFunction, anotherFunction } from './function';

//we can now use our function with the name myFunction because we imported each item
myFunction("Hans Solo");
//output in console = "Hello, my name is Hans Solo"

anotherFunction("Monday");
//output to console = "Today is Monday"
```

This is a good approach on small scale imports (although we can tidy this up a bit more by including all of our exports at the bottom of the page for easy reference). Let's see how that would look -  (the import process will remain the same for this example):

Case #2:

```js
//########### function.js ###########

//we can export each function inline.
function myFunction(name) {
  console.log("Hello, my name is " + name);
  return name;
}

function anotherFunction(day) {
  console.log("Today is " + day);
  return day;
}

export { myFunction, anotherFunction };
```

This method helps us keep track of multiple exports without the need to search the entire page to see what is being exported, but either way achieves the same result.

#### Importing it all

We can also import everything without having to type each single export out in our `import` statement. To do this we can use the `*` operator to signify we want reference to each item being exported from a file. We also use the `as` keyword that gives a base name or alias to our imported items. If we chose to use this method, our "index.js" file would look something like the following:

```js
//########### index.js ##############

//we use * to reference all of the items, we give them a base name, and we call them as a property on that object we import
import * as allFunctions from './function';

//we can now use our function with the name allFunctions.myFunction
allFunctions.myFunction("Hans Solo");
//output in console = "Hello, my name is Hans Solo"

allFunctions.anotherFunction("Monday");
//output to console = "Today is Monday"
```

This method works as well, we simply need to put the name we designate (in this case `allFunctions`) in front of the pieces we are exporting, followed by a `.` and the the name of the exported item (in this case either `myFunction` or `anotherFunction`).


### Exporting classes

Hopefully it will come as no surprise that we can export classes exactly as we would our functions. For instance, if we had a file "classes.js" and had a React class that we wished to export - our file might look something like this:

```js
//########### classes.js ##############

//importing React and Component name for use with our class
import React, { Component } from 'react';

//exporting as a default class for this file
export default class MyCoolComponent extends Component {
  render() {
    return (
      <div>I am Cool</div>
    );
  }
}
```

We could then import this class into another file, let's use "index.js" again :

```js
//########### index.js ##############

//importing React and Component name for use with our class
import React, { Component } from 'react';

//importing Components
import MyCoolComponent from './classes';

class App extends Component {
  render() {
    return (
      <MyCoolComponent />
    );
  }
}
```

Again, we simply export and import and presto, we have access to our other files and their modules. We can use all of the above methods for our classes as we did for our functions.


### Conclusion
* Using `export` allows us to reuse components, classes, functions throughout the entire application and saves us from having to rewrite code over and over again.
* We can export a single item as a `default` export, which gives us access to it's name directly.
* We can export multiple items using the { } notation in our export and import statements.
* We can export an item and rename it using the `as` keyword.
* We can export all of our items using the `*` operator and using the `as` keyword to give it a base name.

#### References
* [MDN export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)
