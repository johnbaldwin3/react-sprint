## Constructor & Instance

* Constructors
In programming, we need to be able to write code that is efficient. Template style code can be used to replicate things without having to write detailed code over and over again. In Javascript, we use constructors to do this. It allows us to be efficient and write clean code.

  {students learn how to create a constructor function in JS and how to instantiate an object with that constructor}

** What is a constructor?
  Any function along with the 'new' keyword, creates an object for which you can define properties and methods. Additionally you can add properties to the constructor using prototypes.

*** the new keyword
  behaviors - adding the word new in front of the constructor name will create a new instance of that constructor
  dangers - not including it will cause you to attach to the window object.

*** props & methods
  All objects have properties and methods on them. Constructors allow you to define these variables and instantiating the constructor you create the specific concrete object.

*** prototype
  Prototype is used to connect properties onto the object - this will be explained in detail in the following lesson.

  var constructor = function(arg){
    this.thing = arg
  }

  var instance = new Constructor("foo");
  console.log(instance.thing) == "foo"
