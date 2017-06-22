## Extending Classes to Sub-Classes
  We have touched on this a little already, but let's trek further into the jungle of Classes and Sub-Classes. We know that Classes are new and cool way to create constructor functions in ES2015 (ES6). One of the cool features we touched on was using the `extends` method to create children constructors, a.k.a sub-classes.

  Another important feature of the new ES2015 syntax is the `set` and `get` methods that come backed in to the new `class` syntax. We will take time to examine those as well. The getters and setters allow us to manage data across our program.

### Creating a sub-class with `extends`
  The primary focus of extend is to easily create prototypal inheritance. Let's take a look at the example below and the flesh out some of the finer details afterwards.

```js
class Animal {
  constructor() {
    this.isAlive = true;
  }
}

class Mammal extends Animal {
  constructor(isAlive) {
    super(isAlive);
    this.hasOrHadHair = true;
  }
}

var dolphin = new Mammal();

console.log(dolphin);
// output => Mammal {isAlive: true, hasOrHadHair: true}
```
So we created a `class Animal` that is a constructor object with the property `isAlive` set to `true`. We then used the magic of the `extends` method to create a `class Mammal` with the property `hasOrHadHair` set to `true`. We used the `constructor()` function to pass in `isAlive` and then the `super()` function to make sure it was inherited from the `Animal` class. If we do not use `super()` we will receive an error because the value of `this` will be undefined. Using `super` points the value of `this` to the parent constructor class.

So we look at the `console.log` output and see that `dolphin` (a new instance of `Mammal`) has the properties from both `Mammal` and `Animal` being inherited.

We could take this one step further and really dive into it... Let's instead create a new `class Cetacean` that `extends` from the `Mammal` class and see what other behaviors we can draw out.

```js
class Animal {
  constructor() {
    this.isAlive = true;
  }
}

class Mammal extends Animal {
  constructor(isAlive) {
    super(isAlive);
    this.hasOrHadHair = true;
  }
}

class Cetacean extends Mammal {
  constructor(hasOrHadHair) {
    super(hasOrHadHair);
    this.marineMammal = true;
  }
}
var dolphin = new Cetacean();

console.log(dolphin);
//output => Cetacean {isAlive: true, hasOrHadHair: true, marineMammal: true}
```

Okay one of the main things to focus on here is the use of `super`. You will notice in the `Mammal` class that we used `super` to reference the parent property `isAlive` on the `Animal` class. When we extended from the `Mammal` class to the `Cetacean` class we used `super` to inherit the property `hasOrHadHair` from the `Mammal` class. By the nature of inheritance we also gained access to the `isAlive` property without having to redefined it in the `super` method again. This is why you can see the `isAlive` property `true` in our output from the `console.log` statement. Wow.. that's deep.


#### What about getters and setters? What can they do?
Every object comes built in with `get` and `set` methods. Both methods do exactly what you would expect.

The `get` method allows us access to property values on an object, where as the `set` methods provides the ability to, as you would expect, "set" property values.

```js
class BluesArtist {
  constructor({firstName, lastName, instrument}) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.instrument = instrument;
  }
  get name() {
    return (this.firstName + " " + this.lastName);
  }
  set name(nameInput){
    var name = nameInput.split(" ");
    this.firstName = name[0];
    this.lastName = name[1];
  }
}

var muddyW = new BluesArtist({firstName: "Muddy", lastName: "Waters", instrument: "Guitar"});

console.log(muddyW.name);
//output => 'Muddy Waters'

muddyW.name = 'Louis Armstrong';

console.log(muddyW.name);
//output => "Louis Armstrong"
```
So what happened? We created a class `BluesArtist` that took in arguments in the `constructor` function. We created a `get name()` method that returned the concatenation of the artist's first and last names. We also provided a `set name()` method that allowed us to pass in a name and change the name of the artist. Just calling `muddyW.name` retrieved the concatenation of names and returned "Muddy Waters". When we provided `muddyW.name` a value to be equal to - `muddyW.name = "Louis Armstrong"` the `set name()` method was invoked and we changed "Muddy Waters" to "Louis Armstrong" as evident in our two `console.log` statements. Neat.

### Conclusion
* Using `extends` on classes allows us to create sub-classes of the parent class. We can inherit properties of those parent classes by calling the `super` method inside of the `constructor` on the child class.
* Using `super` give us access to the value of `this` on the parent class.
* We can use the `get` method to provide access to properties of an object.
* We can use the `set` method to allow us to alter the properties on an object.

#### References
[Getters and Setters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#Defining_getters_and_setters)
