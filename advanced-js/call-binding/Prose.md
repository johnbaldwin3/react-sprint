## Call and Bind methods

In Javascript, functions are objects. As an object, a function can have methods. One of these special methods is called **Bind**. This method is similar to the **Call** and **Apply** methods, but they each have unique qualities which we'll delve into below.


### Apply & Call methods

The apply and call methods allow us to borrow functions and set the `this` value when invoking a function. They are almost identical except that you pass the function parameters to apply () as an array, while parameters passed to the call () method are listed individually. In both methods, the first parameter sets the `this` value to the object that the functions are being called upon. Here is an example:

```js
var person1 = {firstName: 'Leia', lastName: 'Organa'};
var person2 = {firstName: 'Lando', lastName: 'Calrissian'};

function sayHello(){
  console.log('Hello, ' + this.firstName);
};


sayHello.call(person1); // Hello, Leia
sayHello.apply(person2); // Hello, Lando

```

In the above example, call and apply perform the same way. The difference comes up when you want to do something more dynamic with a set of arguments.

```js

function say(greeting){
  console.log(greeting + ', ' + this.firstName);
};

say.call(person1, 'Hello'); // Hello, Leia
say.apply(person2, ['Goodbye']); // Goodbye, Lando

```

In the above example we are passing a greeting in as the second parameter/argument. As you can see, the first parameter is taken as the `this` object, and in the apply method, the second parameter must be passed in as an array. Now let's look at how you can use this unique aspect of this method.

```js
function introduce(greeting){
  console.log(this.firstName + ' ' + this.lastName + ' ' + "I'd like you meet" + names);
};

var names = [" Luke", " Han", " Chewy"];

introduce.apply(person1, names); // Leia Organa I'd like you meet Luke, Han, Chewy

```


### Bind method

The difference between bind and call or apply is that where call and apply execute the function immediately, bind returns a new function.
Where call and apply set the `this` value as the function is being invoked, the bind method sets the `this` value *when* a function or method is invoked, whenever that may be in the future. It's useful for event handlers, when you don't know when the event will be fired, but you know what you want the context to be when they are fired. Let's create a new function that does something later when called:

```js
//create the new function
var sayHelloLeia = sayHello.bind(person1);

//invoke the function later
sayHelloLeia(); // Hello, Leia

```

#### Currying

Bind also allows us to pass further arguments after `this`. In this way it can be especially helpful to curry functions. Let's look at this in another example.

```js
var jediHelp = {
  name: "Jedi Master",
  request: function(help, why){
    return help + this.name + why
  }
};

var obi = {
  name: 'Obi Wan Kenobi'
};

var help_leia = jediHelp.request.bind(obi, "Help me ");

console.log(help_leia(" you're my only hope")); // this logs "Help me Obi Wan Kenobi you're my only hope"
```

See above how we created jediHelp with a generic name (Jedi Master) and set the request method with two parameters. Later we bind the `this` object to a variable we set, along with the first parameter, then later invoke it and pass in the second parameter. Used this way, bind can be a useful tool to allow you write cleaner code.

### Conclusion

In summary, call and apply both invoke the function immediately. Call allows you to pass arguments one by one, apply allows you to pass arguments as an array. Bind returns a new function, and allows you to pass in a number of arguments. All three expect a `this` object as the first argument. Bind is extra useful in currying functions.

#### References

[JavaScript is Sexy](http://javascriptissexy.com/javascript-apply-call-and-bind-methods-are-essential-for-javascript-professionals/?WPACFallback=1&WPACRandom=1417428763444)
[codeplanet](https://codeplanet.io/javascript-apply-vs-call-vs-bind/)
