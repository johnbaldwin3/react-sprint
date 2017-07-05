## Authoring a Reducer to filter data based on a User Action
We've seen the actions, we've seen the reducers, we've seen how they all work together, but let's go a step further and see how they interact together and how we can use a reducer to filter our data based upon a given action. A perfect candidate for this scenario is the timeless classic of a Todo Application! Though we most certainly would not need to actually use Redux to help us manage the limited state of a Todo application, it provides a great platform to simply demonstrate how this process works.

We will assume the usual suspects are to be found in our file tree - we have an app, we've npm installed redux and react-redux, we will have our standard set up of actions, reducers, components, containers directories. We will have used webpack or create-react-app to scaffold our project and have a live server for editing, etc.

So let's first start with creating a list of todos. We should first start with thinking our smart and dumb components, also known as our presentational (regular components) components and our container components. We should recall our container components handle the application state for our entire application, whereas our presentational components handle the state of the user interface, but are not concerned with the data.


### Creating a list of Todos...

We will be using Bootstrap 4 for a few basic styling options, so you might see a few funky class names on our JSX elements, but just understand that those are related to styling.

Our first component we will create will be a container component. It is going to be concerned with the application state of our program because it will be supplying the list of to do items to our todo list components. So in our container folder we will create a file called "CreateTodo.js". This will involve a form that has an input and submit button that will allow us to type our todos in and submit them to our list. Let's take a look at that file:

```js
//############### containers/CreateTodo.js ###############

//import React
import React, { Component } from 'react';

//import connect so we can mesh React and Redux together
import { connect } from 'react-redux';

//redux imports
import { bindActionCreators } from 'redux';

//import an action creator ( we will examine this next )
import { createTodo } from '../actions/index';


class CreateTodo extends Component {
  constructor(props){
    super(props);

    this.state = {
      todoText: '',
    }
  }
  handleInput = (e) => {
    this.setState({todoText: e.target.value});
  }
  handleSubmit = (e) => {
    e.preventDefault();
    this.setState({todoText: ''});
    this.props.createTodo(this.state.todoText);
  }
  render() {
    return (
      <div className="input-form">
        <form onSubmit={this.handleSubmit} className="input-group">

          <input
            type="text"
            className="form-control"
            placeholder="Create a Todo List Item..."
            value={this.state.todoText}
            onChange={this.handleInput}/>
          <span className="input-group-btn">
            <button type="submit" className="btn btn-warning">Create Todo!</button>
          </span>


        </form>
      </div>
    );
  }
}

const mapDispatchToProps = (dispatch) => {
  return bindActionCreators({ createTodo }, dispatch);
}

export default connect(null, mapDispatchToProps)(CreateTodo);
```

The big take away from this file should be the following:
We create two methods (function expression style) `handleInput` and `handleSubmit` that will handle the data that the user puts into our application. We pass in an action creator `createTodo` from our /actions/index.js file that will enable us to keep track of each todo item that is created.

At this point we should have a pretty good concept of what kind of application state our program will need. (This is something we should really flesh out in our wire framing process at the very beginning - to determine who will be a smart component and who will be a dumb component, and what application state we will have).

So let's now go ahead and take a look at our action creators!

### /actions/index.js

```js
//############### /actions/index.js ##################

import { FILTER_TODOS, CREATE_TODO_ITEM, TOGGLE_TODO } from './actions';

//we could have also imported our action types with a universal operator:
// import * as actions from './actions';
// and then in our type declarations we would just have:
// type: actions.FILTER_TODOS (preface actions. for each)

//start id of todos at 0, add one each time a new one is created.
let newTodoId = 0;


export const createTodo = todoText => {
  return {
    type: CREATE_TODO_ITEM,
    id: newTodoId++,
    payload: todoText,
  };
};

export const toggleTodo = id => {
  console.log('id here', id);
  return {
    type: TOGGLE_TODO,
    payload: id,
  };
};

export const toggleFilter = selectedFilter => {
  return {
    type: FILTER_TODOS,
    payload: selectedFilter,
  };
};

```  

So we first import all of our action types from another file (like we would had this been a big program)... we can do that two ways and you can check out the alternative in comments in the code snippet above.

Our entire application will need three types of action creators:

1. **createTodo** : an action creator that creates a new todo when the user submits one, gives it an id, and allows us to pull it from application state to store in a list.
1. **toggleTodo** : an action creator that allows us to cross out our todo items as we complete them. We will be able to click on them and then change the text decoration to have a line through the text. This will also change the complete property from false to true on each todo item.
1. **toggleFilter** : an action creator that will allows us to select from 3 different radio button options (Show All, Show Completed, and Show Incomplete ) - these selections will sort through our todo list based on the completed property of each todo item that is toggled depending on the user's interactions with the list and which items are crossed out.

For each of our action creators we have a type and payload. For our `createTodo` action creator we also add an id property that will incrementally increase with each todo item that is created. You will notice at the beginning of our file, we declare an id property set to zero that we can incrementally increase : `let newTodoId = 0;` and then inside of our action creator we give the id property: `id: newTodoId++` which just adds one to our variable each time we create a todo item.

Now that we have our action creators defined, let's look at our reducers to handle them:

#### Authoring Reducers to create todos and filter todos.
So we really only need two reducers - because the same reducer that will be responsible for creating a new reducer will also be able to track the state of each todo being toggled to completed or incomplete.

Our fist look will be at our root reducer file (index.js) that will combine our reducers into a root file that we can pass to our store in our index.js file.

```js
//############## /reducers/index.js

import { combineReducers } from 'redux';
import toggleReducer from './reducer_toggleFilter';
import todoItems from './reducer_create_todos';

const rootReducer = combineReducers({
  todoItems,
  toggleReducer
});

export default rootReducer;

```

This connects everything to our index.js file that looks like this:

```js
//################# /src/index.js

//react imports
import React from 'react';
import ReactDOM from 'react-dom';
import registerServiceWorker from './registerServiceWorker';

//import styles
import './styles/index.css';

//redux imports
import { Provider } from 'react-redux';
import { createStore, applyMiddleware } from 'redux';
import reducers from './reducers';

//components
import App from './components/App';


const createStoreWithMiddleware = applyMiddleware()(createStore);

//switch uses most specific route that matches, top down.

ReactDOM.render(
  <Provider store={createStoreWithMiddleware(reducers)}>
    <App />
  </Provider>
  , document.querySelector('.container'));
registerServiceWorker();
```

#### Our first reducer...

Our first reducer will be `reducer_create_todos.js`:

```js
//############# /reducers/reducer_create_todos.js ##################

import { CREATE_TODO_ITEM, TOGGLE_TODO } from '../actions/actions';

const todoItems = (state = [], action) => {
  switch(action.type) {
    case CREATE_TODO_ITEM:
      return [
        ...state,
        {
          id: action.id,
          todoText: action.payload,
          completed: false
        }
      ]
    case TOGGLE_TODO:
      return state.map((todo) =>

        (todo.id === action.payload)
        ? {...todo, completed: !todo.completed}
        : todo
      )
    default:
      return state;
  }
}

export default todoItems;
```

At the very top we import our actions, these are simply the strings that will match the action type to the action creator and then match the reducer as well. We import these in our reducer so we have cases to create for our switch/case statement. Next we create our reducer.

We create a function, in this case that will take in state and set it to a default blank array (in the case that our state is undefined, which would throw an error in Redux). It also takes our action as an argument. When it receives all of the action from our dispatch is will pull the action through our switch statement looking at `action.type`.

In the case that the action is `CREATE_TODO_ITEM` we are going to use the spread operator `...` to map through our state and create and return a new array that contains the existing array of state as well. This means that we are able to create a NEW state and not mutate our current state (which Redux would not allow us to do). The second part of our return statement is the new state we would like to merge with the old state. This new state is looking for an id (created by our action), the text `todoText` of our todo item, and setting the completed value to false (since we have just created this todo item).

If the action that is passed through to our reducer is `TOGGLE_TODO` then inside of our return statement, we are going to approach things with the idea being that if a todo item is clicked, then we will find it's id and if the id matches the action id then we are going to toggle the completed value from false to true (if it was false) or from true to false (if it came in as true). We do this by map through our state array (all of our todo items) - we check each todo item to see if it is equal to the action payload (the payload given to the action creator). if they are equal then we use the spread operator to toggle completed (true) to not completed (false) by assigning completed `!todo.completed` or if completed is false, we give it the true value of `todo`.

The last piece of our puzzle is to return a default value of state should none of these cases be matched. We then export the todoItems reducer function.

#### Filtering our Lists

The last big chunk of our puzzle is to be able to toggle one of the radio options (Show All, Show Completed, or Show Incomplete) and be able to filter our list of todo items based on the user's choice of what they would like to see. This will be based on our `toggleFilter` action creator from above - so let's look at the reducer we need to create to make this happen.

```js
//############## /reducers/reducer_toggleFilter.js ################

import { FILTER_TODOS } from '../actions/actions';

const toggleReducer = (state = 'showAll', action) => {
  switch (action.type) {
    case FILTER_TODOS:
      return action.payload
    default:
      return state;
  }
}

export default toggleReducer;
```

In the same fashion as before we will import our action type `FILTER_TODOS` (in this case) and create a reducer function. This function will take in the state and set it to the default value of `showAll`, it will also take in the action. Our switch statement is only concerned with one action type `FILTER_TODOS` and in the case of that being true, we will return the action payload. The `action.payload` in this case is the filter option being passed in from the radio button. This filter option `selectedFilter` will allow us to create a switch statement to pick which todo items should be rendered. This switch statement will be part of our `FilteredTodos` container component which we will look at next. The last part of our switch statement is returning a default value of state.

#### FilteredTodos container component

The `FilteredTodos` container component is our smart component that will match our filter option to a switch case statement that will toggle the view that we render based on what is selected. See the comments in the code for how this all takes place.

```js
//############ /containers/FilteredTodos.js ############

//import connect to connect React to Redux
import { connect } from 'react-redux';

//import our action creator for toggling todo items
import { toggleTodo } from '../actions';

//import our TodoList component concerned with rendering the Todo List
import TodoList from '../components/TodoList';

//create a switch case function named "showFilteredTodos" that receives two arguments.
//1. It receives the todoItems - a list of all items.
//2. It receives the selectedFilter which is one of three things:
// a) showAll (shows all todos without filter)
// b) showCompleted (shows only todos with completed set to true)
// c) showIncomplete (shows only todos with completed set to false)
// we pass these to our cases in the switch and return the appropriate set of list items.
const showFilteredTodos = (todoItems, selectedFilter ) => {
  switch(selectedFilter) {
    case 'showAll':
      return todoItems;
    case 'showCompleted':
      return todoItems.filter(t => t.completed);
    case 'showIncomplete':
      return todoItems.filter(t => !t.completed);
  }
}


//We then need to mapStateToProps, and do setting our todoItems state to the filtered state
//created by our switch statement from above and our toggleReducer function.
const mapStateToProps = state => {
  return {
    todoItems: showFilteredTodos(state.todoItems, state.toggleReducer)
  }
}


//We also need to map our dispatch to props which will take our toggleTodoClick function and dispatch toggleTodo action being passed the id.
const mapDispatchToProps = dispatch => {
  return {
    toggleTodoClick: id => {
      dispatch(toggleTodo(id))
    }
  }
}


//lastly we create our component FilteredTodos and connect our map properties to our TodoList.
const FilteredTodos = connect(mapStateToProps, mapDispatchToProps)(TodoList);

//export for use
export default FilteredTodos;

```

#### ToggleFilters container component
The final remaining container component we need to create is our `ToggleFilters` component that is concerned with the radio buttons that will dictate which list items are rendered. Ignore the classNames, as they are again some styling with Bootstrap 4.

```js
//############### /containers/ToggleFilters.js ###################

import React, { Component } from 'react';
import { connect } from 'react-redux';
import { bindActionCreators } from 'redux';
import { toggleFilter } from '../actions/index';


//create a class based component pass in props via the constructor.

class ToggleFilters extends Component {
  constructor(props){
    super(props);

    //set default UI state for the checkbox next to each radio option
    this.state = {
      selectedFilter: "showAll",
    }
  }
  handleOptionChange = (e) => {
    //pass in the event object and get the value (set to a variable for ease of use)
    let option = e.target.value;

    //set UI state of selectedFilter so the radio button will be checked depending on which option
    //is selected.
    this.setState({selectedFilter: option})

    //send the state to the action creator 'toggleFilter' which will pass the selectedFilter
    //to the reducer when called upon.
    this.props.toggleFilter(option)
  }
  render() {
    return (
      <form>
        <div className="form-check form-check-inline">
          <label className="form-check-label">
            <input
              className="form-check-input"
              onChange={this.handleOptionChange}
              checked={this.state.selectedFilter === 'showAll'}
              type="radio"
              name="inlineRadioOptions"
              id="inlineRadioShowAll"
              value="showAll" /> {"Show All"}
          </label>
        </div>
        <div className="form-check form-check-inline">
          <label className="form-check-label">
            <input
              className="form-check-input"
              onChange={this.handleOptionChange}
              checked={this.state.selectedFilter === 'showCompleted'}
              type="radio"
              name="inlineRadioOptions"
              id="inlineRadioShowCompleted"
              value="showCompleted" /> {"Show Completed"}
          </label>
        </div>
        <div className="form-check form-check-inline">
          <label className="form-check-label">
            <input
              className="form-check-input"
              onChange={this.handleOptionChange}
              checked={this.state.selectedFilter === 'showIncomplete'}
              type="radio"
              name="inlineRadioOptions"
              id="inlineRadioShowIncomplete"
              value="showIncomplete" /> {"Show Incomplete"}
          </label>
        </div>
      </form>
      );
    }
};

// mapping the application state of selectedFilter to props so we can use it set the value of our checked off radio property to true or //false and use it to filter our data.
const mapStateToProps = state => {
  return {
    selectedFilter: state.selectedFilter
  }
}

//mapping dispatch to props we bind our action creator (toggleFilter) to our dispatch function.
const mapDispatchToProps = dispatch => {
  return bindActionCreators({toggleFilter}, dispatch);
};

//we connect our ToggleFilters component to the map functions and export for use
export default connect(mapStateToProps, mapDispatchToProps)(ToggleFilters);
```

We have now wired everything up for use... this is how we filter our data based on a reducer and action creator.
The remaining presentational (dumb) components are simply for displaying this information. We can look at these below with the comments in the code.

#### TodoItem.js
```js
//############## /components/TodoItem.js ##############

//creates a singular todo item to be passed on to the todo list:

import React from 'react'
//if completed is true, we change it's style to have a line through it,
//if completed is false - we give it no special style
//we pass an onClick function to each todo item, that comes from the parent
//component TodoList
const TodoItem = ({ onClick, completed, todoText }) => (
  <li
    onClick={onClick}
    style={{
      textDecoration: completed ? 'line-through' : 'none'
    }}
  >
    {todoText}
  </li>
)

export default TodoItem;
```
#### TodoList.js

```js
//################# /components/TodoList.js ###############

import React from 'react';
import TodoItem from './TodoItem';

//pass in our TodoItem component and our toggleTodoClick function, which will recieve the id
//of the todo item that is clicked.
const TodoList = ({todoItems, toggleTodoClick}) => {
  return (
    <ul>
      {todoItems.map( todo => (
        <TodoItem key={todo.id} {...todo} onClick={() =>{
          toggleTodoClick(todo.id)}} />
      ))}
    </ul>
  )
}

export default TodoList;
```

#### App.js

```js
//############ /components/App.js ##############

import React, { Component } from 'react';
import '../styles/App.css';


//import components
import CreateTodo from '../containers/CreateTodo';
import ToggleFilters from '../containers/ToggleFilters';
import FilteredTodos from '../containers/FilteredTodos';


class App extends Component {
  render() {
    return (
      <div className="App">
        SUPER DUPER FANCY TODO APP
        <CreateTodo />
        <ToggleFilters />
        <FilteredTodos />
      </div>
    );
  }
}

export default App;

```

Now let's checkout how this all looks on the real application!

**INSERT VIDEO/SCREEN CAST HERE*******************
**LINK URL: http://screencast-o-matic.com/watch/cbih2bl2Za**
**INSERT FILE redux-todo-list.mp4**

### Conclusion
* We use our action creators to pass our action to our reducers via dispatch inside of the store.
* The reducers are set of functions that can interpret the action creator functions and manipulate our state according to the action.
* We can use these to filter our data based on certain properties that we pass to our application state.
* Though seemingly complex, the workflow remains the same for all Redux React applications and follows the cycle we have discussed.

#### References
* [Redux Docs Todo App](http://redux.js.org/docs/basics/ExampleTodoList.html)
