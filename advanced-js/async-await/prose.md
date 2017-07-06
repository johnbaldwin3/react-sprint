## Everything but the Kitchen Async.

We just wrapped up learning about generator functions and their role in helping us take asynchronous JavaScript and give it the disguise of synchronous programming. While it all is technically still asynchronous, we found a new power that can tilt our application's behavior into our hands. JavaScript has more tools to help us do that than just pure generator functions. `async` and `await` are two powerful pieces of what we call an `async` function. Async functions are designed to work with the power of generator functions baked in and also go hand in hand with Promises returned from an API.

Let's get our hands dirty and see how we can use async function on a basic level, and then graduate to using them in a promise based example on the next upcoming lesson.

### Creating an Async function

We are going to go into the shallow end to start, so let's just imagine a simple mathematical function that will stand in place for some ajax call that would take an indeterminate and unknown amount of time. We will control the time for this example but we can go to make believe land and pretend that our timeout function is really a stand in for an Ajax call being completed.

Ok.. so.. swimming shorts on, nose plugged, goggles at the ready, let's go! Follow the comments in the code for play by play on the action.

```js

//first we will create a timed function.. this is to mimic what a call to server might be like
function doStuffAfterThreeSeconds(x) {
  //all asynchronous functions return a Promise function
  //Promise get passed a resolve functions (sometimes a reject function)
  //a Promise waits for the return of a value and then is able to do something with it.
  //in this case, we call a setTimeout and return the value of x in our resolve function.
  //We will check out Promises much more in the next lesson.
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(x);
    }, 3000)
  })
}


//we then will create our async function... we use the keyword 'async'

async function addStuff(x) {
  let a = doStuffAfterThreeSeconds(10);
  let b = doStuffAfterThreeSeconds(20);

  //we have called our promise function and passed x a value -->
  //now we need to return those values when they are ready...

  //we call "await" which tells our code to wait for the other functions response to come through.
  return x + await a + await b;
  //we have to call await before a and b because both are linked to the Promise that we are depending on.

}

//now let's call our function and see what happens!!!
//using the .then we won't run our code until the Promise portion has finished.
addStuff(5).then(answer => {
  console.log(answer); //returns 35 after 3 seconds!
});
```

So let's quickly recap and then explore another example. We first defined a function that returned a `new Promise` function. The Promise waits on being successfully run before returning the information needed. Our `await` and `.then` make sure the Promise has run.

We then created an `async function` by calling `async function addStuff()`. Inside we passed our Promise based function two different values and created a return statement with two `await` statements that told our async function to wait until the values were returned before running.

We called our function with a `.then` and passed the value as `answer` and logged it.

Our function ran and the 3000 milisecond time (3 seconds) delayed the function 3 seconds before printing 35 in our console log. COOL!? Right?!

#### I can't believe you would async to that level...
Let's take a look at another example of how we can use our await statements in a different manner ... we can follow along in the comments.

```js
//first we will create a timed function.. this is to mimic what a call to server might be like
function doStuffAfterThreeSeconds(x) {
  //all asynchronous functions return a Promise function
  //Promise get passed a resolve functions (sometimes a reject function)
  //a Promise waits for the return of a value and then is able to do something with it.
  //in this case, we call a setTimeout and return the value of x in our resolve function.
  //We will check out Promises much more in the next lesson.
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(x);
    }, 3000)
  })
}

async function subtractStuff(x) {
  //in this case we will call our await on each individual function call...
  //this should run our doStuffAfterThreeSeconds function two times, with two separate timeouts...

  let a = await doStuffAfterThreeSeconds(20);
  let b = await doStuffAfterThreeSeconds(40);

  return x - a - b;

}

subtractStuff(10).then(answer => {
  console.log(answer);
}); //returns => 10-20-40 = -50 after 6 seconds, because we have run a 3 second timeout twice! COOL!
```

So in the above example, we have used our await statement on our function calls. This calls the Promise function two separate times, thus creating a 6 second timeout as opposed to the three second timeout in the earlier example. So we can see that where we place our await statements are important.

#### The role played, await-ing applause.
So hopefully a bigger picture is coming in to view on how async/await functions can play a huge role in things like fetching data from a server and running callback functions on our clock at the time we want to. Similar to the generator functions, await is a built in pause until ready type process that lets us be sure we have what we need before running a critical piece of code.

### Conclusion
* Async functions are defined using the `async` keyword.
* Inside of an async function `await` lets the function pause and wait for a response from a Promise or other response based function.
* We can use await in more than just the return statement to help determine when our Promise based function will fire and how many times.

#### References
* [Async MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
