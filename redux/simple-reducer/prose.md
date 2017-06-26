## We've Been Reduced to This...
Time for Reducers! We just finished examining and authoring action creators and actions, and we wired them up inside of our container components. But we have yet to see the other side of the mystical cycle of application state in our React Redux project. Let's back track a bit to make sure we can recall our action creators and how we set them up in our last lesson. Once we have those for reference, we can look at creating the final wiring to make everything connect in the cycle.

#### user_detail.js (container component)

```js
//################# container/user_detail.js ################


//React imports
import React, { Component } from 'react';

//our connect function
import { connect } from 'react-redux';

//import our action creator
import { selectUser }  from '../actions/index';

//make sure action created flows through all reducers
import { bindActionCreators } from 'redux';


class UserDetail extends Component {
  //we can add a conditional statement to make sure that if a user has not been selected,
  //we don't receive an error message or have issues rendering this component.
  render() {
    if(!this.props.user) {
      return (
        <div>Select a user to see their details!</div>
      )
    }
    return (
      <div>
        <h3> Details for: </h3>
        <div>{this.props.user.name}</div>
        <div>{this.props.user.bio} pages</div>
      </div>
    );
  }
}

//activeUser reducer (we will examine in next lesson) creates activeUser state.
//this gives us the details for a single user

//Also, since this container component is not concerned with dispatching our action creator, we don't need to
//mapDispatchToProps.

function mapStateToProps(state) {
  return {
    user: state.activeUser,
  };
}


export default connect(mapStateToProps)(BookDetail);

```

### user_list.js (container component)

```js
//################ containers/user_list.js ################

//normal react imports
import React, { Component } from 'react';

//the glue that binds React to Redux so they can communicate
import { connect } from 'react-redux';

//our action creator to select a user
import { selectUser }  from '../actions/index';

//a function that will make sure our action creator is passed to all the reducers to make sure it goes through the right one
import { bindActionCreators } from 'redux';


//for now, just understand that props are coming from the reducer... we will examine that more thoroughly in a coming lesson
//the mapStateToProps function below does this for us.
class UserList extends Component {
  render() {
    let userNames = this.props.users.map((user) => {
      return (
        <li
          key={user.name}
          onClick={() => this.props.selectUser(user)}>{user.name}</li>
      );
    });
    return (
      <ul>
        {userNames}
      </ul>
    );
  }
}

function mapStateToProps(state) {
  //what is returned will show up as PROPS inside of the UserList container
  //inside of this function we generally return an object
  return {
    users: state.users,
  };
}

function mapDispatchToProps(dispatch) {
  //whenever selectUser is called, result should be passed to
  //all of the reducers. (flows through dispatch function -- like a funnel - finding the right reducer for the job)
  //in our return we are binding our action creators to the dispatch function that works behind the scenes for us.
    return bindActionCreators({ selectUser: selectUser }, dispatch)
}

// promotes UserList from component to container and needs to know about dispatch method selectUser (make available as prop)
//this "connects" our functions to our container component and really enables the magic to happen.
export default connect(mapStateToProps, mapDispatchToProps)(UserList);
```

### action/index.js (action creator)

```js
//########### actions/index.js ################
const USER_SELECTED = 'USER_SELECTED';

export function selectUser(user) {
  return {
    type: USER_SELECTED,
    payload: user
  };
};
```

So above we have our two container components, and our action creator with an action. We can review the total details of these in the notes on authoring actions, these are just for reference for how our **reducers** will work.

### The Reducer(s)
We understand that reducers work to take the action creator and action inside of the store and return a new state object to help update our application depending on the action that occurred. In this very simple example, we will have two parts to our reducers.

1. Our main index.js reducer file - this file will combine all of our reducers into one file.
1. Our individual reducer files that will be accountable for each piece of data in our application that needs application state.

Inside of our `reducers` directory we will have three files:
1. reducers/index.js   (our main library of all reducers)
1. reducers/reducer_selected_user.js (the actual reducer for selecting a user)
1. reducers/reducer_users.js (**our hard coded user list** - *this could be generated from an API or our own database in a real app*)

Let's first take a look at the individual reducer files (we can use the convention of naming our file "reducer_name_of_reducer") to help keep track of each file, but it is not necessary. They can technically be named whatever you like - but it is always wise to name with purpose and organization in mind.

#### /reducers/reducer_users.js

Our first stop is very simple, just some hard coded data for our application. As mentioned above this generally would be stored on our database or from another API - but we are just tying to learn about how reducers work so we will keep it simple and hard coded.

```js
//######### .reducers/reducer_users.js ##########


//just a simple function that returns an array of our user objects.
//This is only because we are hard coding data to simplify our example.
export default function() {
  return [
    {
      name: 'Gym Nasium',
      bio: "A big fan of working out and athletics"
    },
    {
      name: 'Cody Coder',
      bio: "Loves to write cool code"
    },
    {
      name: 'Stan Dalone',
      bio: "Not much a social person"
    },
    {
      name: 'Randall Overtheplace',
      bio: "Inspired by Forrest Gump - love to run!"
    }
  ]
};

```

#### /reducers/reducer_selected_user.js
The next file - our very first true reducer is again a function. Let's take a look at how it looks and then explain the pieces of it in further detail.

```js
//############### reducers/reducer_selected_user.js ############

//Our reducer function takes in two arguments
//1. state (which we set to null so we don't get an undefined error)
//2. the action (which we authored previously -
//^ this will be passed from our action creator through dispatch to our reducers)
export default function(state = null, action) {
  switch(action.type) {
    case 'USER_SELECTED':
    return action.payload
  }
  return state;

}
```

We export our function as normal. The function takes two arguments:

1. A state object which we set to null with an ES6 syntax. This syntax states that **if state comes in undefined, we set it to the value of null**. We do this because Redux *will NOT allow state to be returned as undefined*!
1. The next argument is the action. This action is passed from our dispatch (911 call center) from our action creator functions. It is received by all of the reducers and reducer that matches it will process and update state.

We use a switch/case statement inside of our reducer. This switch case matches the action.type to the case type - when the two are equal the return statement is fired and state is updated with the action.payload. In our case, our user is selected, and the payload would be the user's information.

We then have one more return statement that is our default return - that just returns state as it was if nothing is changed. This sets up our individual reducer, but we need to pull all of our reducers together. We do this in our reducers/index.js file. Lets now take a look at that.

### reducers/index.js

Now let's look at how we combine all of our reducers in to one file.

```js
//############# reducers/index.js ###############

// We import the combineReducers function from redux
//this function literally helps us combine all of our reducers
import { combineReducers } from 'redux';

//next we import our individual reducers
import UsersReducer from './reducer_users';
import ActiveUser from './reducer_selected_user';

//create a rootReducer function using the combineReducers function
const rootReducer = combineReducers({
  users: UsersReducer,
  activeUser: ActiveUser,
});

export default rootReducer;

```

We import our `combineReducers` function at the top of the page. We also import our individual reducers next. We then create a variable (function) that is called `rootReducer`. The `rootReducer` becomes our root reducer file - meaning that all of our reducers will be stored here like a root directory.

The `rootReducer` is set to equal a function `combineReducers` which takes in the argument of an object containing each of our reducers and the state they are associated with. Our users state is associated with our hard coded users data reducer. The activeUser state, is associated with our selected user reducer that we named `ActiveUser` in the index.js file.  So when we select a user, we fire an action, which goes through dispatch in the store and funnels through the reducers. When the action type matches the switch case statement in our reducer, we return a new state object. `activeUser` was the name we gave to our updated state back in our user_detail.js file in the `mapStateToProps` statement at the bottom, where we determined that the selected user state would come from the activeUser key that we created in our reducer.

It's a big circle back to re-render our application with updated state - but everything has now been wired and linked together and this program would allow a user to click on a list item (user) and render the details of that user.

This is obviously way over simplified - and this application certainly would not *need* Redux to manage application state since there is so little of it, but this is the ground work for building bigger and better apps!

### Conclusion
* Reducers work in tandem with the action creators to update application state and re-render our components in React via our container components.
* Reducers are simply functions that take in state and action and update the state according to the action.
* We create reducers for each action, and then combine them in a rootReducer file (reducers/index.js).

#### References
* [Redux](http://redux.js.org/)
