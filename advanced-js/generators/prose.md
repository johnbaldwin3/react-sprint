## Generator Functions
We have been diving in the waters of advanced JavaScript, and the waters feel good hopefully! The powerful additions of ESNext syntax, ES6 most specifically, are designed to make our workflow easier and accomplish more with less code. Well, it's time to take a look at a new fish in the JavaScript sea. Generator functions. Generator functions are a means to help handle the asynchronous nature of JavaScript and put the control of the asynchrony in the hands of the programmer. Generator functions are able to be entered and exited over and over again, with their progress being saved across each entry to the function.

These generator functions serve us in the real world during things like testing, callback functions, promises related to server requests, etc. We will focus on what they are at a very basic level in this lesson and continue to expand on them in the lessons to come.

### How do we create a Generator function?

Let's first examine how we create a Generator function and then begin the conversation of what it is doing more in depth. We create generator functions with a few primary keywords to focus on. The first step is creating the function itself. With regular JavaScript functions we would do something along the lines of :

```js
function myFunction(arg1, arg2) {
  return arg1 + arg2;
}
```

To create a generator function, we use the `function*` keyword.

```js
function* myGeneratorFunction(optionalParams1, optionalParams2) {
  //to be discussed shortly
}
```

What goes on inside of the generator function is different than what you would expect to find in a regular function. We make use of the `yield` keyword which allows us the ability to stop and start our function with each call, it also returns an object that has a value property and a done property for the entire generator (set to a boolean value). The `done` property lets the generator know to keep going. **It's also important to know that when we define our generator function, we are creating a constructor function, but not one that is defined by the `new` keyword, yet it must still be instantiated before it's use** It's creating a Fruit - we wouldn't go to the store to buy a Fruit, we would go to the store to buy an Apple, or Mango, etc. The Apple and Mango in this example are the defined instantiations of the constructor. Once we create the instantiated function, we use a special `.next()` function to run our generator one time and exit after saving the results.

So let's go back and look at our generator function and see it put to work as kind of a simple arbitrary example:

```js
function* myGeneratorFunction() {
  //define an index
  let index = 0;
  //while index is less than 4, return yield function which will run index++ one time and save the results
    while(index < 4) {
      yield index++;
    }
}

//We must now instantiate our Generator constructor object.
const indexMaker = myGeneratorFunction();

//we can now run our generator function indexMaker and log the results in console.log() statements:
//we run our generator function by calling the next() function on it. We can get value from using ".value"

console.log(indexMaker.next().value); //****** output returns => 0
// the first call of the function will start the function... it will execute from the beginning of the function until the first yield ( basically saying stop here! ) statement, thus the reason why we return 0 first.

// we can call it again to make our generator run another time:
console.log(indexMaker.next().value); //****** output returns => 1
// and again
console.log(indexMaker.next().value); //****** output returns => 2
// and again
console.log(indexMaker.next().value); //****** output returns => 3

//something special happens after our conditions for running have been met, we will now return undefined to stop the loop
// and again
console.log(indexMaker.next().value); //****** output returns => "undefined"
// we return undefined because now index is greater than 4
```

Let's checkout another example to see it in action again going further in depth on how the generator function works:

```js
//create our generator function
function* stopByReturn() {
  yield "I will run, and my done property will be false";
  yield "I will run too, and my done property will be false"
  return "I will run also, but my done property will be true"
  yield "I won't run, and will be undefined, boohoo :( "
}

//instantiate it
const stopMyFunc = stopByReturn();
console.log(stopMyFunc.next()); //first run : return => { value: "I will run, and my done property will be false" , done: false }
console.log(stopMyFunc.next()); //second run : return => { value: "I will run too, and my done property will be false" , done: false }
console.log(stopMyFunc.next()); //third run : return => { value: "I will run also, but my done property will be true", done: true }

console.log(stopMyFunc.next());
//fourth run: return => undefined (It didn't run because the return statement stopped our function)
//returns the object { value: undefined, done: true }
```

So we can stop our function with a return after a desired amount of yields have been run, we also will stop the function after our yields have all completed. This also shows a means in which we pass arguments into a generator. For instance:

```js
function* logItAllGenerator() {
  console.log(yield);
  console.log(yield);
  console.log(yield);
}

var gen = logItAllGenerator();

// the first call of next executes from the start of the function
// until the first yield statement
gen.next(); //initializes our function
gen.next('cowboy'); // returns => "cowboy"
gen.next('cowgirl'); // returns => "cowgirl"
gen.next('cow'); // returns => "cow"
gen.next('cowardly') // does not run....because we have yielded three times already
```
When only passing in one argument, `yield` will automatically return that argument. The above function is the same as :

```js
function* logItAllGenerator(param1) {
  console.log(yield param1);
}
```

We can also pass another generator function into the yield statements of a different generator function like so using the `yield*` keyword which tells yield that it will be passed a generator function:

```js

//create one generator function
function* anotherGenFunc(x) {
  yield x + 10;
  yield x + 11;
  yield x + 12;
}

//create another generator function that incorporates the first
function* addGen(x) {
  yield x + 1;
  yield x + 2;
  yield* anotherGenFunc(x);
  yield x * 10;
}

//assign x to myGen function instantiation
const myGen = addGen(5);


//log through next() statements:
console.log(myGen.next().value); // returns 5+1 = 6
console.log(myGen.next().value); // returns 5+2 = 7
console.log(myGen.next().value); // returns 5 + 10 = 15 (from anotherGenFunc)
console.log(myGen.next().value); // returns 5 + 11 = 16 (from anotherGenFunc)
console.log(myGen.next().value); // returns 5 + 12 = 17 (from anotherGenFunc)
console.log(myGen.next().value); // returns 5 * 10 = 50
console.log(myGen.next().value); // returns undefined because all yields have occured.
```

So this is a brief intro into how to create generator functions and how they work... but we haven't really answered the why part of it yet.

#### So where would we see generator functions in the wild?
Generators are JavaScript's way of answering to "callback h-e-double-hockeysticks" aka "callback hell". It allows us to take out the uncertainty of asynchronous actions. We can use generator functions to make sure something asynchronous like an Ajax call will follow on a timeline and path that we choose and only complete on our terms and not get lost in the call stack.

### Conclusion
* JavaScript is an asynchronous language, and that fact can give us problems in predicting when certain code will run.
* New ES6 / ESNext syntax allows us to create a sense of synchronous functionality by allowing us to enter and exit out of a function when want to.
* Using `function*` allows us to declare a generator function.
* Using `yield` allows us to run code up until each yield is met in the code.
* We can use `yield*` to yield another nested generator function.
* We use `.next()` to start our function and run it up until each corresponding yield statement.
* Using return in the generator function will exit the generator and not complete any futher yields.

#### References
* [David Fox Powell Medium Blog (includes profanity)](https://medium.com/@dtothefp/why-can-t-anyone-write-a-simple-es6-generators-tutorial-ec2bbdf6ff45)
* [MDN Generator Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)
* [Alex Perry article](https://alexperry.io/javascript/2015/09/17/es6-generators-and-asynchronous-javascript.html)
