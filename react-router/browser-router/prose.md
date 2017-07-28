## Using BrowserRouter to Enable Browser History

In the past, with React Router, to avoid using hash based routing and to use resource routing we had to jump through a few hoops. We don't need to go into specifics but just understand it was not as easy as it is now. React Router version 4 has made life much simpler for us.

### Enabling All of the Things

We discussed the difference between hash-based routing and resource routing. React makes life simple by taking the best of both worlds. What this gives us is the ability to track the history of our application within the browser and at the same time render our routes dynamically and with speed like hash-based routing.

By enabling the history API in the browser, we can track a users endpoints and allow them to get back to a previous page by using the back button and send links to other people that will direct those people to the exact contact the original user wanted them to see.

#### The Set Up

Lucky for you, we have really covered the necessary set up to do this. React Router's new `<BrowserRouter>` component has the history API weaved into it. To use it, we must wrap our entire sections of routes with it. If we only want to render one route at a time in our page, which may or may not be the case depending on the complexity of our app, we will need to use the `<Switch>` component. The `<Switch>` component is an exclusive route provider (**exclusive rendering**) - meaning it seeks the route that matches the path and when it finds it, it stops looking and rendering anything else. This will be our focus for awhile with our apps as we learn to render multiple different pages as a SPA (Single Page Application). The alternative would be to use **inclusive rendering**, in which all routes are displayed on a page. 

Ok, to review, let's check the code:


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


//wrap our <Route> components with <BrowserRouter> component.
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
```

It's that easy - we now have access to the browser's history API and we can let our users successfully navigate our application and be able to return to each endpoint as they wish or direct other users to the same endpoint.

### Conclusion
* Using React Router 4's `<BrowserRouter>` component, we automatically gain the ability to use the history API.
* The allows users to use the back button in the browser to return systematically through the application on the path they used to get there.
* This also allows the user to send links to specific endpoints with the ability to show another user the same content.
* We use the `<Switch>` component when we want to ensure that only one route will be displayed at a time. This is *exclusive rendering* as opposed to *inclusive rendering* where all routes would be displayed.

#### References
* [Switch Component](https://reacttraining.com/react-router/web/api/Switch)
* [BrowserRouter](https://reacttraining.com/react-router/web/api/BrowserRouter)
