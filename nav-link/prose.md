## Active Navigation Links with React Router
React Router gives us a lot of really helpful tools, you should be chomping at the bit with excitement and wonder for all of the ways we can apply these wonderful additions. Just like some infomercial tagline of old "But wait, there's MORE!" - React Router has even more to offer us. We are going to examine the concept of active navigation links and how we can style them in React Router easily and efficiently using `<NavLink>` components.

### The NavLink component.
In the following basic example, we are going to create a very simple "SPA" that will have a very minimal navigation bar. This navigation bar will be present on all of our pages (because we want it to be) and should help direct us to the other portions of our application while also signaling what current page we are on.

#### The set up...
Looking inside of our index.js file, we are going to see that really not much more work was required for this addition to our project. We simply can add `NavLink` to our list of imported components from `react-router-dom`. We then will call that component to create a Navigation Bar style element that has some really cool attributes available to use. Let's look below:

```js
//########### index.js ##############
import registerServiceWorker from './registerServiceWorker';

//import React
import React from 'react';
import ReactDOM from 'react-dom';

//import Styles
import './styles/index.css';

//import React Router
import {BrowserRouter, Route, Switch, NavLink} from 'react-router-dom';

//import Components
import App from './scripts/components/App';
import PageOne from './scripts/components/page_one';
import PageTwo from './scripts/components/page_two';

ReactDOM.render(
  <BrowserRouter>
    <div>
      <div className="nav-bar">
        <NavLink activeClassName="selected" className="nav-menu" exact to="/">Main</NavLink>
        <NavLink activeClassName="selected" className="nav-menu" to="/page_one">One</NavLink>
        <NavLink activeClassName="selected" className="nav-menu" to="/page_two">Two</NavLink>
      </div>

      <Switch>
        <Route path="/page_one" component={PageOne} />
        <Route path="/page_two" component={PageTwo} />
        <Route path="/" component={App}/>
      </Switch>
    </div>
  </BrowserRouter>

  ,
  document.getElementById('root'));
registerServiceWorker();
```

It's *important* to note that inside of our `<BrowserRouter>` we are still limited to return one child element, as we are inside of any of our component render methods. So in order to make this style of code valid, we must wrap both our `<NavLink>` and `<Switch>` components in an outside `<div>`.

We will come back to this later on, and look at refactoring the `NavLink` component filled Navigation Bar and making it a stand alone component that can be reused wherever we see fit. But first let's just get a good overhead view of what is going on.

Inside of our `<div className="nav-bar">` we have passed several `<NavLink>` components. Each <NavLink> component has a few baked in attributes that we are able to call upon to make our life easier.

We won't use all of these for this example, but here are the attributes that `<NavLink>` has:
1. `activeClassName: [[takes a string " " as value]]` - the activeClassName will check against the url in the browser and when it matches it will add on a special class name that you define (a common one would be "selected" or "active"). This allows us to set a CSS style for the active class, which will allow us to easily see what link is active compared to the others.

1. `activeStyle: [[ takes an object { } as a value ]]` - the activeStyle attribute will take an object {} filled with style key value pairs. For instance if we wanted our active link to change font color and background color we would pass activeStyle an object like so -

```js
<NavLink
  activeStyle={{
    color: "blue",
    backgroundColor: "white"
  }}>Main Page</NavLink>
```
1. `exact` is a boolean value that we have seen before. The `exact` keyword is placed before the `to=` path declaration. This means that in order for any of the other attributes to be true, the path URL must match exactly to the `to=` attribute.


```js
<NavLink activeClassName="selected" className="nav-menu" exact to="/">Main</NavLink>
```

The above snippet would mean that if, and ONLY if the path was just "/" would any of the attributes work.

1. `strict` can be used to make sure that each path has a trailing "/": for instance - `/home/`. We wont dive much deeper into this right now, but know that it exists and would take the place of `exact` in terms of placement in the `<NavLink>`.

1. Lastly, we have the `isActive: [[takes a function as a value]]`. This will take a 

#### [Child-Subsection Title]
[Content for each child-subsection subject in an objective.]
### Conclusion
[Summary of content covered]
#### References
[Resource links]
