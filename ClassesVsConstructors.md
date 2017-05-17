## ES2015 Classes vs. ES3 Constructors
  With the unveiling of ES2015 (sometimes referred to as ES6) syntax, JavaScript made its way toward becoming a class based object oriented programming language, at least above the water. However, what is really going on behind the scenes is a new and shiny method to create constructors the old way but using the new `class` syntax to do so. Let's take a look at some of the fundamental differences and similarities between `class` and constructor functions.

### What is a constructor function?

Well by now we have learned what constructor functions do and how they operate. Very simply put, constructors allow us to create objects that will inherit methods and properties from parent objects using the prototypal chain.

If you recall the Fruit example we've already gone over:

```js
function Fruit() {
  this.sweet = true;
  this.hasSeeds = true;
}

function Apple() {

}

Apple.prototype = new Fruit();

var apple = new Apple();

console.log(apple.sweet);
//output => true
```

We created a `Fruit()` constructor function, and then defined an `Apple()` constructor function and using the `Apple.prototype = new Fruit()` we allowed `Apple` to inherit from the prototypal chain of the `Fruit` constructor.

### So now what is a `class`, and how can it help us?

Classes are really just a fancy table cloth for the table of constructors and prototypal based inheritance that we already know. They provide us with a means to more simply and clearly create objects and deal with their inheritance. Classes are special functions that can be expressions or declarations as with any function. Let's look at a *class declaration* first. There a few new key words that we will need to be familiar with and point out along the way with the new syntax. Keep an eye out for

  - `class`
  - `constructor`
  - `extends`
  - `super`

as we move through the examples. We will be sure to point them out as they pop up.

We will also take note of JavaScript's hoisting properties and sub-classes as well.

#### Class Declaration
  Reinventing the Fruit?

```js
  class Fruit {
    constructor(data) {
      this.sweet = data.sweet;
      this.texture = data.texture;
    }
  }

  var apple = new Fruit({sweet: true, texture:'crunchy'});

  console.log('apple.sweet', apple.sweet);
  //output => true
  console.log('apple.texture', apple.texture);
  //output => "crunchy"

```

So what happened? Well, we created a `class` called `Fruit`. This `Fruit` class acted as our constructor function, and in fact you can see that we used the function `constructor()` to set up how our constructor function would pass down properties. Now in this example, for the sake of showing how it worked, we left our `sweet` and `texture` properties empty and then assigned them value when we instantiated a `Fruit` instance with the variable `apple`. We simply passed the key value pairs to the `new Fruit()` function and as a result you can see the ouput from the `console.log` statements reflected those values.

### Let's take it to the next level!
  Already you should be getting a taste for how nice and clean the table cloth looks on that dusty constructor table. Classes provide us with a new efficient and clean method to create inheritance. But we can go even farther by diving in to the world of *sub-classes*. Let's take a look at a new example... you're probably tired of fruit, so here's something that eats fruit instead.

```js
  //First let's create a class called Primate
  class Primate {
    constructor() {
      this.isMammal = true;
      this.isSmart = true;
      this.opposableThumbs = true;

    }
  }

//Now let's create a SUB-CLASS called Monkey using the extends and super keywords
  class Monkey extends Primate {
    constructor(name, color, isMammal, isSmart, opposableThumbs) {
      super({isMammal, isSmart, opposableThumbs});
      this.name = name;
      this.color = color;
    }
  }

//Now let's create an instance of Monkey
var spiderMonkey = new Monkey({name: "Spider Monkey", color: "black and brown"});

//We've given the Monkey constructor some key value pair information
//Let's see if spiderMonkey inherited from the Primate constructor by using "super"

console.log(spiderMonkey.isMammal);
//output => true

```

So what happened? Alot! First let's look at the `extends` keyword. We are able to create a `Monkey` sub-class by typing `class Monkey extends Primate`. Well `extends` does just that, it extends a constructor's inheritance to the new constructor or instance.

Now if we examine the `constructor` function in the `Monkey` class, you'll notice that we passed along quite a few parameters. We gave `Monkey` new properties of `name` and `color` that were not present in the `Primate` class, but we also passed along the parameters that we wanted to carry on from the `Primate` class, such as `isMammal` and so on.

That's all well, but if we were to try to reference them just as so, we would get a reference error. That's where the `super` function really does a super job of helping us with inheritance. Using `super` and passing it the properties and methods from the parent constructor class allows us to retrieve those inherited properties and methods.

That's why when we `console.log(spiderMonkey.isMammal)` the output we get in return is `true`!!! How cool is that!?

#### Class Expressions

Hopefully there really is not much mystery left in classes, and class expressions work very much like a function expression and can be both **unnamed** and **named**. Let's take a look.

```js
  //Let's create an UNNAMED class expressions
  var Monkey = class {
    constructor(color, name) {
      this.color = color;
      this.name = name;
    }
  }

  //By comparison a NAMED class expression looks like this:
  var Monkey = class Monkey {
    constructor(color, name) {
      this.color = color;
      this.name = name;
    }
  }

```

And that's that... the named class expression uses the `class Monkey` whereas the unnamed class expression uses the anonymous `class { }`.

#### Hoisting! Heave... Ho.. Heave.. Ho..
We have learned previously that JavaScript uses hoisting to lift variables and functions up on its first pass through the script so that they can be referenced anywhere. Well.. unfortunately that same hoisting **DOES NOT** apply to classes.

Here's a look :

```js
//the following variable will throw a reference error and the code will not run because the class is not hoisted above it.
var mono = new Monkey(); // :( !!

class Monkey {
  constructor() {
    this.doStuff = true;
  }
}
//Monkey would need to be defined above any instance it is called to make for the code to work.
class Monkey {
  constructor() {
    this.doStuff = true;
  }
}

var mono = new Monkey(); // :) !! Will WORK!!! Hooray Monkey!

```
#### Static methods on classes..
 The new `class` syntax also has access to `static` methods. Static methods are designed to live only on the constructor they occur on and not be passed down to any children. We will also take a look at how to apply default properties to a constructor as well.

 For instance:

 ```js
 class Chameleon {
   static colorChange(newColor) {
     this.newColor = newColor;
   } //below we set a default of green to the constructor like so
   constructor({ newColor = 'green'} = {}) {
     this.newColor = newColor;
   }
 }

let pantherChameleon = new Chameleon({newColor: "purple"});

console.log(pantherChameleon.newColor);
//output => purple

pantherChameleon.colorChange("orange");
//output => Uncaught TypeError: pantherChameleon.changeColor is not a function
console.log(pantherChameleon.newColor);
//does not run
 ```
So the changeColor function only works for the Chameleon object. We did set the default to green above, but, we have other issues.
If we were to have instead written:

```js
Chameleon.colorChange.call(pantherChameleon, "orange");
console.log(pantherChameleon.newColor);
//using the call function we can apply the colorChange function to the pantherChameleon
//output of the console.log statement => "orange"
```

By using the `call` which will learn more about later, we can attach the `colorChange` function to `pantherChameleon`, but this isn't ideal... instead we would be better off by re-writing our static method to allow for children objects to use it, and bypass the call method altogether, like so:

```js
class Chameleon {
  static colorChange(lizard, newColor) {
    lizard.newColor = newColor;
  }
  constructor({ newColor = 'green'} = {}) {
    this.newColor = newColor;
  }
}

var pantherChameleon = new Chameleon({newColor: "purple"});
Chameleon.colorChange(pantherChameleon, "neon blue");
console.log(pantherChameleon.newColor);
//output => "neon blue"
```

You can see the static method still keeps the function `colorChange` locally, but by allowing the parameter `lizard` to take place of `this`, we can replace the `call` function and simply pass in `pantherChameleon` as an argument.


### Conclusion

* JavaScript's ES3 constructors and new ES2015 classes essentially do the same things.
* Classes provide a clean method to use prototypal inheritance and create object constructors.
* A `constructor` function must be used in order to determine what code will be run when creating a new instance of the constructor object.
* Classes can easily make sub-classes and pass inheritance using the `extend` keyword and the `super` function.
* The `super` function allows for a child object to inherit methods and properties from the parent object.
* Classes are **NOT** hoisted, and therefore will throw a reference error if an instance is declared before the class.

#### References

[Resource links]
