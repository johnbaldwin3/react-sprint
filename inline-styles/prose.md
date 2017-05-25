## Altering the Styles of Components with Inline React Styling
We've concentrated a lot on the building of components and data flow in terms of `state` and `props`, but man oh man, our websites have been pretty ugly so far. We haven't concentrated much on the styling aspects that are available to us when building React applications. The availability to style things based on a class or using inline styles in HTML has long been a tool for software engineers. React allows us to do the same sort of styling inside of our components within our JSX elements. It's functionality is not much different, though some of the properties and declarations need to be a little bit different to function in the weird hybrid world of JavaScript and XML (JSX).

Reacts foundation centers around modularizing (creating stand alone pieces of code) our code and really making everything self-contained. That is why we use JSX, so that we don't have to write components, and then HTML, and then JavaScript, and have multiple files all effecting one singular component. React takes the same view on styling. Why have multiple sources of styling? It would not allow for self-contained UI components, which pretty much goes against the grain of React!

Let's take a look on the approach React suggest for our styling process and keeping everything nice and tightly contained within our components.

### classNames for Style!
In HTML, just as in JSX, we have the ability to designate class (HTML) or classNames(JSX). First let's see the HTML approach and then we will examin how to manage the same situation with React.

Imagine we have a very plain chunk of HTML with a few class names.

```HTML
<body>
  <nav>
    <header class="header">Header</header>
  </nav>
  <div class="cool">
    <h3 class="sweet">Amazing stuff here</h3>
  </div>
  <div class="cool">
    <h3 class="sweet">Amazing stuff here</h3>
  </div>
  <div class="cool">
    <h3 class="sweet">Amazing stuff here</h3>
  </div>
</body>
```
Given the above HTML, we could very easily style our differnt elements using CSS. In our CSS stylesheet, we might have the following for example.

```CSS
.header {
  color: red;
}
.cool {
  background-color: blue;
}
.sweet {
  color: white;
}

```

Pretty simple and should be complete review. We create classes and then we target those classes within our stylesheet and alter them according to our design wishes. No problem there.

Now, let's think of a React component, and how we would tackle the same thing.

```js
class App extends Component {
  constructor(){
    super();
  }
  render(){
    return (
      <body>
        <nav>
          <header className="header">Header</header>
        </nav>
        <div className="cool">
          <h3 className="sweet">Amazing stuff here</h3>
        </div>
        <div className="cool">
          <h3 className="sweet">Amazing stuff here</h3>
        </div>
        <div className="cool">
          <h3 className="sweet">Amazing stuff here</h3>
        </div>
      </body>
    )
  }
}
```

As you probably guessed, our CSS stylesheet would be the *EXACT* same as before. We can freely target any of the classes that we wish and alter their stylings.

```CSS
.header {
  color: red;
}
.cool {
  background-color: blue;
}
.sweet {
  color: white;
}

```

So, pretty simple, right? Well, we still didn't quite keep everything self-contained, as a React purist might suggest. So let's take a look at how we would make all of our work with a UI component happen in one tidy little place. This is where things take a slight change and we encounter some new stuff.

### Inline Styling
In HTML, inline styling is definitely a thing, and in fact, it takes precedence over all other styling usually. We could for instance style an `<div>` tag as such: `<div style="color : green;">This is a Green Heading</div>`.

Well, essentially we can do just that in our JSX, but there a few rules for the road we ought to check out before we drive.

1. Single worded CSS properties like **"border"**, **"color"**, **"width"**, all will remain *unchanged* and used just as they would be in CSS.
1. Mulit-word CSS properties (usually with a dash in between them) such as **"text-align"**, **"font-family"**, or **"background-color"** must now adhere to JavaScript standards and become "camelCased" (that is to say, all one word, with the first word being lowercased and the second being stuck on the end but capitalized.).
  * Our previous examples would then become: **textAlign**, **fontFamily**, and **backgroundColor**.

So let's take a look at a couple of ways we can apply this for inline styling.

#### Create a variable

Inside of our `render` method before our `return` statement we can actually apply our styling into a variable and then pass that variable to our elements as need be. This might be the best choice if a lot of styling needs to be done to a whole component (and not lots of tiny elements). We then add a `style` attribute to the element or component in question and pass our variable in as the value using `{}` brackets: `style={yourVariableHere}`.
```js
class App extends Component {
  constructor(){
    super();
  }
  render(){
    let headerStyle = {
      color: "red",
    };
    let coolStyle = {
      backgroundColor: "blue",
    };
    let sweetStyle = {
      color: "white",
    };
    return (
      <body>
        <nav>
          <header className="header" style={headerStyle}>Header</header>
        </nav>
        <div className="cool" style={coolStyle}>
          <h3 className="sweet">Amazing stuff here</h3>
        </div>
        <div className="cool" style={coolStyle}>
          <h3 className="sweet">Amazing stuff here</h3>
        </div>
        <div className="cool" style={coolStyle}>
          <h3 className="sweet">Amazing stuff here</h3>
        </div>
      </body>
    )
  }
}
```

That's pretty cool, and pretty handy, but a bit clunky at times. We could also create a property and then pass it value inside of the variable we created. For instance, each `<div className="cool">` is styled to have a blue background, but what if we wanted that a bit more adaptable/customizable. We can create a `bgroundCol` (or whatever you want to name it that makes sense) and apply that to each div. We then would use the `props` to pass the value to our variable in charge of styling. Let's see it in action:

```js
let headerStyle = {
  color: "red",
};
let coolStyle = {
  backgroundColor: this.props.bgroundCol,
};
let sweetStyle = {
  color: "white",
return (
  //snippet from total example
<nav>
  <header className="header" style={headerStyle}>Header</header>
</nav>
<div className="cool" bgroundCol="blue">
  <h3 className="sweet">Amazing stuff here</h3>
</div>
<div className="cool" bgroundCol="green">
  <h3 className="sweet">Amazing stuff here</h3>
</div>
<div className="cool" bgroundCol="brown">
  <h3 className="sweet">Amazing stuff here</h3>
</div>
  //snippet end
  )
}
```

By passing our `backgroundColor:` property the value of `this.props.bgroundCol`, we are able to style directly inline as we see fit! Cool, right?

#### Totally inline!

We can take it one step further and actually style completely inline as well. Let's take a small piece and see how that might look.

Let's really jazz up a new `<div>`... we simply give it a `style` attribute and pass in our properties as an object, like so:

*Note that double brackets : we are passing our first set of brackets an object containing our styling*

```js
<div className="new" style={{color:"orange", backgroundColor: "purple", fontSize: "33px", textAlign:"right", height: 80}} >Im the best Div ever </div>
```

* The majority of the properties that involve a default value of pixels (px) can either be put in as a string "33px" or "33", or a straight number such as `80`. The compiler knows to add 'px' on the end when it renders. (There are a few exceptions that you may find).

That's all there is to it, you should be spooled up and wired to go for styling within your components now!

### Conclusion
* React purists feel that all of the creation, including styling, should be contained with a UI component.
* In React, we can style by using the `className` attribute and then using our CSS or Sass stylesheet to transform our component.
* We can also style directly inline with React. This can be done one of two ways:
1. Creation of a variable that is passed to the `style` attribute, containing an object filled with our style properties and values. We can also pass props from our element or component to our style variable to make it more customizable.
1. Styling directly inline with our element or component passing in an object filled with the style properties and values.
* Multiword style properties should be camelCased (`backgroundColor`). The only exceptions are the `data-` and `aria-` properties, that remain separated by a dash.

#### References
* [Kirupa.com](https://www.kirupa.com/react/styling_in_react.htm)
* [React Docs](https://facebook.github.io/react/docs/dom-elements.html)
* [React JSX](https://facebook.github.io/react/docs/jsx-in-depth.html)
