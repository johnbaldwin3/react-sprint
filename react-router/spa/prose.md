## A Relaxing Day at the SPA...
We've discussed Single Page Applications before, (sometimes referred to as SPAs), and the benefit they present to making web applications. They give us the ability to load more quickly, retain data without the need to refresh, and make the journey and experience of the user much more streamlined. It's now to time to add another tool to our React tool belt which will make the design and implementation of SPAs much easier to deal with.

React Router. A router, in terms of a web application, is comparatively like an air traffic controller at the airport in a few different ways. The air traffic controller (ATC) makes sure that all of the planes know when to take off and land and overall makes sure they don't run in to each other. A router does a similar job, it helps organize the routes in which our web application should follow and directs the user or data inputs to the appropriate portions of our web application.

ATCs also make sure things run efficiently at the airport and try to maximize the flow of traffic so things keep moving. Our router does the same thing. A router is designed to intercept information that would normally go to the server, decide what to do with it, and in the case of React, determine which components should be rendered. That ability to stop communication from going all the way to the server really speeds up our applications and lets us work much more efficiently.

With all of this in mind, let's get the scoop on React Router, and how to integrate it into our applications.

### Installing React Router
Assuming we have already set up a `create-react-app` application, or used a webpack with the necessary goods for a React application, we will start there with an empty application.

The first thing we will need to do is go into our terminal and `cd` into our project directory. For this mock up, lets pretend we are in `/TIY/code/router-project/`.

We are going to use npm to install React Router with the following code (again, in our project directory) :

```
npm install --save react-router-dom
```

This will install all of the React Router dependencies for a *web application* that we need to get going inside of our project. The current version of React Router this lesson is based off of is **version^4.1.1**.

### Thinking about our application...
There are a couple of ways we can think about utilizing React Router in our SPA, but all of them really boil down to a few details.
1. Whether we are using a component or our index.js, React Router is the single source of output for our application.
  * That means that all of our application will flow through our routing components in order for React Router to work.
1. React Router will require the use of a few different key components working together.
  * We will examine the `<BrowserRouter>`, `<Route>`, `<Switch>`, and the `<Link>` components employed by React Router v4.

For this really simple application we will begin in our `index.js` file where we normally just have a `ReactDOM.render()` statement that plugs our app into the container `<div>` in our HTML.

#### index.js
Inside of our *index.js* file, let's look at the set up for our app and how we incorporate the beginnings of our React Router app.

First we are going to see our normal list of React dependencies (React and ReactDOM) being imported, as well as our style sheet. Underneath our styles import, we see the importing of React Router with the `{BrowserRouter, Route, Switch}` dependancies specifically.

```js
//######### index.js #############

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

ReactDOM.render(
  <BrowserRouter>
    <Switch>
      <Route path="/page_one" component={PageOne} />
      <Route path="/page_two" component={PageTwo} />
      <Route path="/" component={App}/>
    </Switch>
  </BrowserRouter>

  ,
  document.getElementById('root'));
registerServiceWorker();
```

Looking at the code above, we can see that inside of our `ReactDOM.render()` statement that we have a component wrapping our entire application called `<BrowserRouter>`. The `<BrowserRouter>` is a router that uses the HTML5 history API to keep the UI of your application in sync with the URL the user is on. The `<BrowserRouter>` allows us to return a single container for our application as is required in JSX.

The next component we see inside of `<BrowserRouter>` is the `<Switch>` component. `<Switch>` allows us to to render a `<Route>` (which we will discuss shortly) based on a specific set of criteria, i.e. an exact URL match.

The `<Route>` component is exactly what you expect - it specifies the URL route that should excist for a given component. It has two major attributes the `path=` and `component=`. The `path` attribute takes the name of the route that should exist for a given component, for example, `path='/page_one'`. The `Route` components should be listed in order of specificity. The most complex routes being listed first, whereas the least complex should be listed last. This is because `Switch` will match the route to the first criteria that it finds to fit the bill.

#### The order of routes
Let's look more closely at that and pretend that we had written the first route component with a `path='/'`.

```js
<Route path="/" component={App}/>
<Route path="/page_one" component={PageOne} />
<Route path="/page_two" component={PageTwo} />

```

`Switch` would then look at our application, and since every route begins with a forward slash `/` they would all match the first route component. Therefore no other route would be rendered no matter what the URL was. Thus, we list the `path="/"` `<Route>` last and it allows each component to be read and matched before finding a component that is just a slash.

We could make one change to this by using the `exact` path keyword. In the above example, where our routes are ordered from least complex to most, we could add `<Route exact path="/" component={App}/>` to our first Route and therefore only if the path was a `/` would it be matched. There are problems with this logic however, especially when dealing with complex routes that are dynamic in nature (changing with data or input). The dynamic routes might fail to yield the expected results when using `exact`, so it is best practice to order our routes from most to least complex, to avoid issues.

```js
<Route path="/page_one" component={PageOne} />
<Route path="/page_two" component={PageTwo} />
<Route path="/" component={App}/>
```

#### The component to be rendered
As you can see from our very first code snippet, we also imported the components from our other files in our list of import statements.

These import statements allows us to utilize that component inside of our router (just as we could render them normally before a router). The second part of the Route component is the  `component={}` attribute. Simply passing in the name of the component (as we imported it to be) tells the router to render it when the correct path is met as a URL. So when we have the URL "`example.com/page_one`" we expect our path to math the first `<Route>` component and display the `<PageOne>` component to the user.

### A look inside of the component
Now lets bust a move on over to our `page_one.js` file (in our mock app) where our `<PageOne>` component is being exported from.

At the top of the page you will see our normal imports of React and React Component.

Then next major part of React Router is seen in the following import state `import { Link } from 'react-router-dom';`.

The `<Link>` component is unsurprisingly exactly what is sounds like, a link. This takes the place of our normal anchor tags `<a>` (but actually renders an anchor tag in HTML) and comes with a few baked in goodies.

```js
//######### page_one.js #############

import React, { Component } from 'react';
import { Link } from 'react-router-dom';

export default class PageOne extends Component {
  render() {
    return (
      <div className="App one"><div className="header">Page One!</div>
        <p className="para">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
        <div><button className="btn"><Link to="/">Main Page</Link></button></div>
        <div><button className="btn"><Link to="/page_two">Page Two</Link></button></div>
      </div>
    );
  }
}
```

For this example, we have wrapped our `<Link>` component inside of a button element, for UI purposes. The real take away here is what goes on with `<Link>` though.

```js
<Link to="/page_two">Page Two</Link>
```

The `<Link>` component has one primary attribute: `to=`. It simply specifies the route to which that link should take the user via React Router. Here on our `PageOne` component we have links to our `MainPage` component and our `PageTwo` component inside of the two `<Link>` components. We can utilize any method we have already learned to provide text for our Links in between the opening and closing `<Link>` tags - we kept it simple here with plain text, but could have easily added some sort of JavaScript by using `{}`.

It's important to know that what is actually rendered by the `<Link>` component is an anchor tag `<a>` for styling purposes, though we could pass a `className` to each link as well. In this instance, we could have styled the anchor tags by doing the following:

```css
/*******STYLE SHEET********/
.btn a {
  text-decoration: none;
  font-size: 20px;
  color: black;
}
```

Here we have a `className="btn"` for each of our `<button>` elements and inside of those we have the anchor tag which we style via regular CSS in the above code snippet. Reminder: This could be nested using Sass!

### The end result
Let's take a look at the simple three page application (with minimal styling for demonstration) that can be acheived with React Router:

**INSERT VIDEO: url(http://screencast-o-matic.com/watch/cbhvD8XGGh) or filename:(/reactrouter.mp4)**

### Conclusion
* React Router allows us to create simple and efficient single page applications.
* We can use npm to install React Router for web applications by typing: `npm install --save 'react-router-dom'` in our project folder in terminal.
* The `<BrowserRouter>` component allows us to use the history API for the browser, which in later projects we will examine the importance of.
* The `<Switch>` component allows us to match a `path=` to a `component=` and render that component only when the path matches the exact router specified.
* We organize our `<Route>` components by complexity of their `path=""` attribute. The more complex routes are listed at the top and the least complex are listed at the bottom.
* Each `<Route>` component has two main attributes - the `path` and `component`. The path attribute is the URL endpoint we which to match against for our component to render. The component attribute is the component we wish to render when the path is matched.
* Inside of our application components, we can import the `<Link>` component which will create an anchor tag element when rendered. `<Link>` takes a `to=""` attribute and specifies the path to which the user should be taken to upon some sort of event (click, etc.).

#### References
* [React Router](https://reacttraining.com/react-router/web/guides/quick-start)
