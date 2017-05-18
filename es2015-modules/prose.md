## Modules... Super Heroes of ES2105
 Modules came about as a means to get rid of global variables, which could wreak havoc on large programs, or programs with multiple authors. Prior to ES2015 syntax, modules were available in ES5 by coupling requireJS and using `require` statements at the top of a page where you wanted to bring them in. Exporting was done in a similar fashion at the bottom a file using `module.export` statements.

 Well ES2015 is here, and as Bob Dylan once said, "The times, they are a changin'"... The new syntax really simplifies the whole process and allows for streamlined importing and exporting of code between pages.

### Export to Import.. simple as that.

 Let's say that I have a file, "utility.js", that holds a few different utility functions that I plan to use in multiple places. By using the `export` command we can export one or multiple files. To bring them into another file we simply use the `import` method as seen below.

 ```js
//###### utility.js #######
export function makeMath(x,y) {
  return ( x * y );
}

//then on our index.js page...

//###### index.js ########
import makeMath from './utility.js';

console.log(makeMath(2,3));
//output => 6
 ```

It's pretty much that easy... we can import one or multiple pieces of data this way as well. Let's take a look at how we would do that.

```js
//###### utility.js #######
export function makeMath(x,y) {
  return ( x * y );
}

export function makeFood(meat, cheese) {
  return ("You've got a " + meat + " sandwich with " + cheese +  " cheese.");
}

//then on our index.js page...

//###### index.js ########
import {makeMath, makeFood} from './utility.js';

console.log(makeMath(2,3));
//output => 6

console.log(makeFood("salami", "gruyere"));
//output = > "You've got a salami sandwich with gruyere cheese"
```

With multiple files we simply add `{ }` around the files we are importing in, such as `makeMath` and `makeFood`.
If we had a ton of files to export and import from a single file, that might be a bit time consuming. We handle that situation by using the `*` operator.. let's take a look at that in action. For the sake of space we will just re-examine our previous approach.

```js
//###### utility.js #######
export function makeMath(x,y) {
  return ( x * y );
}

export function makeFood(meat, cheese) {
  return ("You've got a " + meat + " sandwich with " + cheese +  " cheese.");
}

//then on our index.js page...

//###### index.js ########
import * as utility from './utility.js';

console.log(utility.makeMath(2,3));
//output => 6

console.log(utility.makeFood("roast beef", "cheddar"));
//output = > "You've got a roast beef sandwich with cheddar cheese"
```

Above you can see that we used the `*` and coupled it with a new keyword `as` to allow us access to all files being exported `from` our './utility.js' file.

This literally says: "Hey I want to take everything from this file and name it as *utility* to access later on"

We simply need to place the `utility.` in front of any of the function, variables, etc that we plan to use and import from that utility.js file. For example: `utility.makeFood("ham","swiss")` Easy peasy lemon squeezy, right?

You can also still export everything from the end of a file like we did in ES5. Instead of using `export ...` for each function, variable, etc. You could place an export statement at the bottom of the file like so:

`export { makeMath, makeFood }` This would achieve the same results.


### So what are the benefits of this?

 Well for starters we can eliminate issues with global variables. We can also start to organize our code in to reusable pieces. This is a huge part of things to come and tidy programming in general.

### Conclusion
* Using `export` allows to ship pieces of code or entire files to other files within our program.
* To retrieve those files we simply call `import` in the file that we wish to use them.
* We can import multiple pieces of code by using the `import { myFunction, myVariable, myArray} from './myFile.js'` or -
* We can import them with a generalized method by using `import * as myThings from './myFile.js'`
* We would then reference those files by means of `myThings.myFunction` or `myThings.myVariable`.
* Imports are hoisted, that is to say, that it doesn't really matter where you call them within a module, but it is good practice to keep all import statements together at the top.

#### References
[ExploringJs](http://exploringjs.com/es6/ch_modules.html)
