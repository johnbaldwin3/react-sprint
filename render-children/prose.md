## Rendering Child Components in React
Inheritance in React can be a tricky thing. Considering the way React builds things, some components may not even be aware of the children components they will have later on. How do we tackle this problem? Let's take a look...

### Consider a BaseLayout Component
Let's think for a minute that we have a component that consists of our Navigation Bar and our Footer that we would like rendered on almost every page.

```js
class BaseLayout extends Component {
  constructor(props) {
    super(props);
  }
  render() {
    return(
      <div>
        <nav>some stuff here</nav>

        <footer>some more stuff here</footer>
      </div>
    );
  }
}

```

This is a very simplistic view, but let's think about what is going on here. We've got a main div that holds both our navigation and footer elements (which most certainly could be components on their own as well).

What if, at the same time, in our main App.js file we had something along the lines of this...?

```js
class App extends Component {
  render(){
    return (
      <BaseLayout>

      </BaseLayout>
    )
  }
}
```

How would `<BaseLayout></BaseLayout>` be able to render any other components that needed to go between (inside of) the navigation and footer elements? The majority of our content is likely to live there, but how?

#### Use props.children !
In order to pass components *or elements* into another component that may not know what it's children are going to be, or may render many different children depending on the page, we use `{props.children}`
This allows for a component to render things passed into it, and doesn't require that the component even reside inside of the same script sheet.

Let's take a look at how this works and what this means...

First let's pretend that our `<BaseLayout />` component lives in a file called **baselayout.js**.

```js
//################## baselayout.js ##############

import React, {Component} from 'react';

export default class BaseLayout extends Component {
  constructor() {
    super();
  }
  render(){
      return (
        <div className="base">
          <nav className="navbar">
            <h3>Navigation Bar: A cocktail lounge for coders</h3>
          </nav>

          {this.props.children}

          <footer>
            <div className="footer-div">
              <h5>This is the BaseLayout footer...</h5>
            </div>
          </footer>
        </div>


      );
    }
  }
```

So, here is what we've got for our `<BaseLayout>` components. A few things to take note of:
* We again are reminded that only one container (`<div className="base"> </div>`) may be returned in a component.
* We see in the portion that would equate to the "body" of the page that we use brackets `{}` and pass in `{this.props.children}`. We use the `constructor()` and `super()` functions in order to receive access to the "props" and the `this` object.
* Another reminder, We could have written this component as a function:

```js
function BaseLayout(props) {
  return (
    <div className="base">
      <nav className="navbar">
        <h3>Navigation Bar: A cocktail lounge for coders</h3>
      </nav>

      {props.children}

      <footer>
        <div className="footer-div">
          <h5>This is the BaseLayout footer...</h5>
        </div>
      </footer>
    </div>
  );
}
```

**If we did write this as a function, we no longer are required to use `this` in front of `props.children`**

Let's also take a look what is going on in our **App.js** page.

```js
//################ App.js ####################

import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

//import components
import BaseLayout from './Components/baselayout';

export default class App extends Component {
  constructor(props){
    super(props);
  }
  render() {
    return (

        <BaseLayout>
          <div className="main">
            <h4>This is the body!</h4>
          </div>
        </BaseLayout>

    )
  }
}
```

* Inside of our `<App />` Component, you can see we pass in `<BaseLayout>` from our import statement as a pair of tags (`<BaseLayout> </BaseLayout>`).
* Inside of our `<BaseLayout>` tags we are able to pass elements or other components!
* Our **baselayout.js** file tells the the `<BaseLayout>` component to expect children elements or components because of our `{this.props.children}` statement.

The output you would expect to see from this simple demonstration (plus very minor styling):

![props children](./children.png)


### Conclusion
* We can render child components in React by using `{this.props.children}` or `{props.children}`, depending on if we are creating a `class` or `function`.
* `{this.props.children}` allows a component to receive other elements or components without really requiring the component to predict which or what will be rendered.
* We could use our `<BaseLayout>` tags in multiple pages and be able to render relevant material to each page because we are passing the `{this.props.children}` to the portion of the component we wish those children to be rendered in.
* This flexibility leads to more reusable code and the ability to keep our code DRY!

#### References
[React Components](https://facebook.github.io/react/docs/composition-vs-inheritance.html)
