## Functions & Prototypes

Functions are a critical part of Javascript. They allow us to reuse functionality throughout our applications and make up the core of what programming is all about. A powerful tool in Javascript is the prototype, which allows you to pass properties and methods down to other functions.

#### Defining a function
By now you know how to write functions. A function is defined (also called function declaration or function statement) using the `function` keyword, followed by the name of the function, parentheses enclosing the parameters, and curly brackets with encasing what the function does.
For example:

```js
function addTwo(number){
  return number + 2;
}
```

And remember that functions are just specialized objects. So we can add functions as methods inside an object. This function declaration without a name is called a function expression.

```js
var thing = function(param){
  return param;
}
```

We can assign a function to a variable and pass that variable as an object. Since we can pass objects as regular variables, it makes sense that we can attach functions as properties of Javascript objects. A function on an object is referred to as a 'method'.

```js
  var thing = {
    one: function(){
      return makeMischief;
    },
    two: function(){
      return makeMoreMischief;
    }
  }
```

#### Binding an object to the prototype

Every function in Javascript has a prototype. Being an object, a function will inherit properties and methods from it's prototype. Similar to how you learned that properties on the 'Fruit' object can be passed using prototypal inheritance (example below), methods can also be passed along in this way.

```js
function Fruit() {
  this.sweet = true;
  this.hasSeeds = true;
}

function Apple() {
  this.texture = 'crunchy';
}

Apple.prototype = new Fruit();

console.log('Apple.prototype:', Apple.prototype);
// output => 'Apple.prototype: Fruit {sweet: true}'
```

An example of passing a function as a method on the prototype of an object:

```js
Fruit.prototype.biteMe = function(){
    console.log("once bitten, twice shy")
}

var pear = new Fruit();

console.log(pear.biteMe()); //logs "once bitten, twice shy"

```

#### How `this` works in binding Methods

Remember that with constructors `this` is always the new object being constructed. So any methods attached to `this` in a constructor are attached to that new Object. This is where prototypes can come in handy. Let's say we wanted to add a method to a constructor:

```js
function Const(par1, par2){
  this.par1 = par1;
  this.par2 = par2;
  this.someMethod = function(){
    return this.par1 + " " + this.par2;
  };
}
```

While the above may look logical, there are two issues with writing it this way.
1. Binding a method to `this` inside the function object provides it only to that particular instance.
2. any method attached this way will get re-declared for every new instance created, negatively affecting memory usage if you are creating many instances.

Prototypes to the rescue!

If you apply the method to the object's prototype, it is only stored in the memory once, and all instances of that object will have access to that method.

```js
function Const(par1, par2){
  this.par1 = par1;
  this.par2 = par2;
}

Const.prototype.someMethod = function(){
  return this.par1 + " " + this.par2;
};
```

While there are advantages to using the prototype approach, how you write code will always depend on the situation. There may be times when you will need to access local private variables for a method, for which the first example would be a preferred method.

#### Conclusion

Functions can be defined in a few different ways. When you attach a function onto an object it's called a method. Methods can be inherited the same way that properties can using prototypal inheritance.

#### References

[Javascript is Sexy](http://javascriptissexy.com/javascript-prototype-in-plain-detailed-language/)
