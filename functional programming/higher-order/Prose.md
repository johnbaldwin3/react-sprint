## Higher Order Functions

A function, at its simplest, is "a block of code designed to perform a particular task". In JavaScript, functions are specialized instances of objects that we can invoke to perform an action or compute a value. Since a function is an object, it can be assigned as the value of a variable or passed and returned just like any other variable. A higher-order function is one that takes one or more functions as an argument.

### Callback functions

A callback function is a higher-order function - a function that is passed to another function as a parameter, and executed inside that function. It's important to note that when the function is being passed in, it is merely the function definition - we are not executing the function in the parameter. The function is being "called back" later inside the other function's body, hence the name "callback". A callback gets executed at the end of an operation, once all of the other operations have been completed. It's usually passed in as the last argument, and frequently defined inline as an anonymous function. A simple example:

```js
$('.button').click(function(){
  alert("button clicked");
});

```

Passing in a function to be executed after the parent function's operations are completed allows for **asynchronous** behavior. This means a script can continue running while waiting for a result. *This is a very important behavior when dealing with resources that might return a result after an undetermined period of time.* An example of this is when you make an Ajax request to a server. You don't know how long it will take to get that response back, and need the script to keep running while waiting for the response. This can also be helpful when waiting for user input to perform a function.

Callback functions are **closures**. When passed in as an argument into a function, a callback is executed inside the function body the same as if it was defined inside the body, meaning it acts as a closure. Remember, closures have access to the scope of the function they are contained within, so this means the callback can access the parent function's variables as well as the global scope variables.

#### "Callback Hell"

Sometimes you will end up with multiple callback functions nested inside each other. At a certain depth, you will enter "callback hell" - called this because of how difficult it will be to follow the code due to the number of callbacks. Try to avoid falling into these depths! Instead of using anonymous functions `function()` be sure to name our functions and just pass the name of the function into the parameter `function Name(param1, function1Name)`. Another thing many coders do that will keep your code clean and organized is to separate your code into modules. This allows you to export that section of code that does a specific job and import it where you need it in your larger application.

### Conclusion

- A higher order function is one that takes another function as an argument (a callback function)
- Passing in a function as a parameter allows for asynchronous programming
- Callback functions are closures, meaning you can access all the variables of the parent function
- Avoid callback hell by naming your functions and passing in the name only or separating code into modules

#### References

[Sitepoint](https://www.sitepoint.com/higher-order-functions-javascript/)
[JavaScript is Sexy](http://javascriptissexy.com/understand-javascript-callback-functions-and-use-them/)
