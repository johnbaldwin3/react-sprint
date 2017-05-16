##  Prototypal Inheritance

  All functions in JavaScript have prototypes, though some just remain undefined. The prototypes of an object allow new objects to inherit properties in a hierarchal fashion from other objects. This transfer of methods and properties between multiple objects can be referred to as Prototypal Inheritance, Prototype-Based Inheritance, or Delegation.

### It all starts with the Object
 In JavaScript all Objects are created with methods and properties right out of the gate. All new objects inherit these properties from the JavaScript Object.

 Fun things like `Object.prototype.toString()` or `Object.prototype.valueOf()` are just a few of the goodies that come pre-packaged on the prototype of the JavaScript Object.

 These properties are passed down automatically to all objects created in JavaScript. This is the very basics of prototypal inheritance.

### How does inheritance work?
  Let's take a look at a constructor function called `Fruit`.
  ```js
function Fruit() {
  this.sweet = true;
}
```
We can give `Fruit` properties directly such as a `sweet`, by using `this.sweet = true` as seen above.

Now let's see how inheritance works. Let's create a new constructor called `Apple` which will become a child of the Fruit constructor.
```js
function Apple() {
  this.texture = 'crunchy'
}
  ```
#### As of right now...
The `Apple` does not inherit anything from the `Fruit` constructor, so if we were to check to see if the apple was sweet, it would be undefined. To make the apple sweet, we need to set up inheritance as follows...

```js
Apple.prototype = new Fruit();

console.log('Apple.prototype:', Apple.prototype);
// output => 'Apple.prototype: Fruit {sweet: true}'
```
#### So what happened?
  The `Fruit` constructor passed it's properties down the prototypal chain to the new instance `Apple`. This is why `console.log` returns `Fruit` and it's properties.

  But it doesn't end there, remember those freebie prototypes from the JavaScript Object? Well let's look below... we have not defined a `valueOf()` method anywhere, and yet if were to run the following code, you can see the output below gives us a value! COOL, that's inheritance at work again!
```js
  console.log(Apple.prototype.valueOf());
  // output => Fruit {sweet: true}
```

#### One step further...
  Prototypal chains can continue even further - let's look at the following:
  ```js
  var apple = new Apple();

  console.log('apple.texture:', apple.texture);
  //output => 'apple.texture: crunchy'
  console.log('apple.sweet', apple.sweet);
  //output => 'apple.sweet: true'
  ```
  The reason that `apple` is crunchy *stems* from the fact that it inherited crunchy from the `Apple` constructor when the `var apple = new Apple();` was instantiated. But what would have been impossible without prototypal inheritance was for `apple` to also be sweet without the declaration of `Apple.prototype = new Fruit();`

  #### Is that the only way? Nope!

  Another example of inheritance can be demonstrated by using the `Object.create()` method. Let's take a look at a variable named `parent` with a function `sayName` and see how it can be passed down to it's child (a variable name `child`) and used by the child variable.

  ```js
  var parent = {
    sayName: function() {
      console.log('Hey my name is ' + this.name);
    },
    name: 'ParentPerson'
  }

  var child = Object.create(parent);
  child.name = "PersonChild";

  //Because of inheritance . . .
  child.sayName();
  //console.log output => "PersonChild"
  ```
#### What's really happening here?
  Behind the scenes when the `child.sayName()` is invoked, the `child` object is first examined for the `sayName()` function, when the function is not found there, JavaScript searches up the prototypal chain and the next stop is the `parent` object, at which point `sayName()` is found. `sayName()` then runs on the child element, using the name property from the `child` object where it was called.

### Conclusion
 Prototypal inheritance is a very powerful tool in JavaScript that allows us to pass methods and properties between object constructors.
