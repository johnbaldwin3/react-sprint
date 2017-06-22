## How to Incorporate a Layout Component into Our React App
We are up and running with React Router, and we have looked a very simple application and the use of a router to navigate around it, so it's probably time to start diving deeper into the functionality and common layouts within an application. Think of just about any webpage you would can imagine... usually there is some piece of the webpage that renders on each part of the webpage you visit - whether it's a navigation bar, a simple logo, or something more complex such a search bar, these elements are visible on multiple pages and commonly referred to as a layout component. Let's take a look at how we can style a very simple logo and title bar at the top of a simple application.

### It's not an empty nest anymore...
The way we accomplish this layout component is by nesting child components. We have already done this, hopefully a few times, by this point, so we are going to concentrate more on how this is accomplished using React Router. React Router gives us a lot of extra power to navigate our app, but we need to make sure we handle nesting our components properly so that we can render everything correctly.

So first stop on this adventure is to create a layout component, since this will be the base of all pages on our application, we will call it `<BaseLayout>` and we will create a new file called `base-layout.js` to export it from.

```js
//############ base-layout.js ##############
import React, { Component } from 'react';

export default class BaseLayout extends Component {
  render() {
    return (
      <div>
        <div className="header">
          <h1>Bill Murray</h1>
          <p className="bill">In Bill We Trust</p>
        </div>
        {this.props.children}
        <footer><h5>Murray Rocks</h5></footer>
      </div>

    )
  }
}

```

Nothing too fancy pants about this, we are creating a container `<div>` to return from our `render` method and inside of that we have a `<div className="header">` and a `<footer>`. In between these two sections, we are passing in `{this.props.children}`, which as you recall, will allow us to render different components inside of this layout.

#### Bringing it all home
Since we know we want to display this `<BaseLayout>` on each of our application pages, we need to look at our `index.js` file since we are using React Router. We know that inside of our `<BrowserRouter>` we can only return one child element, so let's peek in and see how to manage this with our `<BaseLayout>` component.

```js
import registerServiceWorker from './registerServiceWorker';

//import React
import React from 'react';
import ReactDOM from 'react-dom';

//import Styles
import './styles/index.css';

//import React Router
import {BrowserRouter, Route, Switch} from 'react-router-dom';

//import Components
import App from './scripts/components/App';
import PageOne from './scripts/components/page_one';
import PageTwo from './scripts/components/page_two';
import BaseLayout from './scripts/components/base-layout';

ReactDOM.render(
  <BrowserRouter>
    <BaseLayout>
      <Switch>
        <Route path="/page_one" component={PageOne} />
        <Route path="/page_two" component={PageTwo} />
        <Route path="/" component={App}/>
      </Switch>
    </BaseLayout>
  </BrowserRouter>

  ,
  document.getElementById('root'));
registerServiceWorker();
```

The meat and potatoes of this magic happens inside of `<BrowserRouter>`. We simply import our `<BaseLayout>` component in the list of other components we are importing, and then use it to wrap the `<Switch>` component, which wraps our `<Route>` components. By doing this we still only return one container inside of `<BrowserRouter>` and our `<BaseLayout>` is ready for rendering child components because of the `{this.props.children}` that we gave it back in our `base-layout.js` file.

So let's take a look how this would appear with minor styling. We would expect to see the `<BaseLayout>` being rendered on each page...

Here is our main `<App>` component page:

![main](./main.png)

Now let's see if we still render it on the `<PageOne>` component:

![p1](./p1.png)

Yep! We have successfully introduced a layout component and displayed it with nested child components in our web application. Cool!

### Conclusion
* We can use a component dedicated to a certain layout to display on multiple pages using React Router.
* Passing the layout component `{this.props.children}` ensures that it will always be able to render other components inside of the layout.
* With React Router, we can use the layout component as a container to wrap all of our `<Route>` components and our `<Switch>` component.
