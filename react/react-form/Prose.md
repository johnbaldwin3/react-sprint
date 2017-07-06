## Implementing a Form on a React component

Now that we've taken the plunge into React, we've got a grasp of some of the basic fundamentals. How do we make it actually do something useful? We want to interact with the user and be able to capture their input and do something with that. Forms are a great tool to do this. Forms in React are a little different, in that the HTML form elements already hold some internal state. Let's demonstrate making a simple form in React to collect the user's name. We'll go through the process of creating the form step by step, and then put it all together at the end.

### Collecting Input

To collect input from the user, first you need to create a Form component, and since we expect the data to change, we will use *state* to manage the input (rather than *props*). Remember when we first create the component we can initialize the state of the component. You'll remember from previous lessons and exercises that we create a React component by extending it on a `class`. Then we use the `constructor` method to initialize the state and include the `super` function to ensure that the value of `this` is pointed to the parent constructor class.

```js
class Form extends React.Component {
  constructor(props){
    super(props)
  }
}
```

As you'll remember, components must always have a `render` function. This tells React what to display in the DOM. And the `render` function should return a single React element. We could write it like this:

```js
render(){
  return (
    <form>
      <input name="name" type="text" value="name" />
    </form>
  )
}
```

However, this would mean that the *value* is always set to "name" and cannot be changed by the user. To allow the user to change the value, we can make it dynamic by allowing it to be updated from the state:

```js
render(){
  return (
    <form>
      <input name="name" type="text" value={this.state.name} />
    </form>
  )
}
```

Now in order for React to know when a user changes the value of the state for that element, we need to add an event handler to capture the change:

```js
handleNameChange(event){
  this.setState({name: event.target.value})
}
```

This event handler is placed in the code above the render method. The 'event' is the user typing into the input form. This 'event' is passed into the handler, and you then target the value that is being changed in that event, and use the `setState` method to update the state with the changed value.

You can name event handlers whatever you want, but it is general practice to use the word 'handle' along with the change that it is dealing with, so called ours *handleNameChange*.

But wait, how is the event being passed in? We need to use the `onChange` function to capture the change in input:

```js
render(){
  return (
    <form>
      <input name="name" type="text" value={this.state.name} onChange={this.handleNameChange}/>
    </form>
  )
}
```

Now that we've added the `onChange` function, we need to bind it to the `this` of the component. If we forget to bind the `this` the handler is being called on to the `this` of the component, it will cause an error as `this` will be undefined:

```js
this.handleNameChange = this.handleNameChange.bind(this);
```

The above code needs to be written inside the constructor method of the component. And since the constructor method is where we set the initial state, we can set the state of the name input to an empty string, as we are expecting the input to be text. Let's put those both into the constructor:

```js
class Form extends React.Component {
  constructor(props){
    super(props)

    this.handleNameChange = this.handleNameChange.bind(this);
    this.state = {name: ''};
  }
}
```

Okay, we're making progress. But we're missing one thing. Since this is a form, a natural user expectation would be that when they hit the enter key, the information they just typed should be submitted. So let's create an event handler to handle the form being submitted, that shows them an alert when they submit:

```js
handleSubmit(event){
  event.preventDefault();
  alert('Thank you, ' + this.state.name + 'your name was submitted');
}
```

Note that we used the special `event.preventDefault()` method here. Most people's natural tendency is to hit the enter button after typing in some text, but most of the time you will have more than one input field in a form, and the default behavior when hitting the enter key is that the form is submitted. This would not be what you would want to happen if there are additional fields the user needs to fill out before submitting. So get in the habit of placing this function in your handleSubmit on the forms you create to avoid submitting the form too early.

The last bit we need to add is the same thing we did with our other event handler - we need to bind it to `this` in the constructor. Then our React component will be ready for the red carpet.
Here is the final version, ready for the paparazzi:

```js
class Form extends React.Component {
  constructor(props){
    super(props);

    this.handleNameChange = this.handleNameChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);

    this.state = {name: ''};
  }
  handleNameChange(event){
    this.setState({name: event.target.value});
  }
  handleSubmit(event){
      event.preventDefault();
      alert('Thank you, ' + this.state.name + 'your name was submitted');
  }
  render(){
    return (
      <form onSubmit={this.handleSubmit}>
            <input onChange={this.handleNameChange} name="name" type="text" value={this.state.name} />
        </form>
    )
  }
}
```



### Conclusion

When making a form in React, you can connect the input changes to the state. Initialize the state in the constructor method. Target any changes, as well as the submittal of the form, with an event handler. Use the `setState()` method to update the state and re-render. Make sure to bind the event handlers to `this` in the `constructor` method. And don't forget to use the `preventDefault()` function to avoid early submittal of the form.

#### References

[Site point](https://www.sitepoint.com/work-with-forms-in-react/)

[React Forms](https://facebook.github.io/react/docs/forms.html)
