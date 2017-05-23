## Passing Data via Props to Child Components
We have taken a dip into the waters of React, but haven't really gotten our hands dirty as of yet. It's time to get into some of the finer details and start to peek at the way data is passed around between components. You may or may not be surprised to find that you've already been doing this in previous examples. We're just going to go more in depth on *how* these processes work.

Since each component should be responsible for small pieces of the puzzle, it's unlikely that one component will hold all of the data management and distribution for a project - in fact - it definitely should not. We should have a lot of "dumb" components that inherit their properties from "smart" components. Each should be individualized so that the code can be plugged into and reused in the project multiple times if need be.

### The List App
Since these are complex ideas, we need to make sure we really get a good grasp and understanding of what is going on behind the scenes. The following example is not some amazing magically cool project, but it will definitely allow us to see the bigger picture about passing props between components and the functionality we gain by doing so.

Let's envision an application that simple writes a list for you. Maybe a class list maker for a teacher?
Before we even look at code, let's think about the parts of this application (and understand that some are not broken down as far as they could be for the ease of illustration).

* We would need some means to enter a student's name (a form!) with a button to submit that name to a list of students.
* We then would want some visual representation of this list, let's actually just use a simple unordered list for this example.
* When we enter the students name, it will be pushed into an array of students, and then we will pass that array down to the component that renders the list on our web page.

No, it sure isn't the craziest most complex program ever built, but it will give good insight into the inner workings of React components and their properties.

#### The App build
Let's first examine the higher component, which contains the form that we will input students names into, and grasp what is occurring there.

```js
export default class App extends Component {
  constructor(props){
    super(props);

    this.handleName = this.handleName.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);

    this.state = {
      students: [],
      name: "",
    };
  }
  handleName(e){
    this.setState({name: e.target.value});

  }
  handleSubmit(e) {
    e.preventDefault();
    this.state.students.push({studentName: this.state.name});
    this.setState({students: this.state.students, name: ""});

  }
  render() {
    return (
      <div className="class-maker">
        <h3>Create Your Class List Here: </h3>
        <form onSubmit={this.handleSubmit}>
          <input type="text" onChange={this.handleName} value={this.state.name}/>
          <input type="submit" value="Add Student" />
        </form>
        <StudentList students={this.state.students}/>
      </div>
    );
  }
}
```

There is a lot going on here, so we will break portions of this into bite size chunks and tackle them one at a time.

Our first stop is going to be the `render()` method on our `<App />` component.

```js
render() {
  return (
    <div className="class-maker">
      <h3>Create Your Class List Here: </h3>
      <form onSubmit={this.handleSubmit}>
        <input type="text" onChange={this.handleName} value={this.state.name}/>
        <input type="submit" value="Add Student" />
      </form>
      <StudentList students={this.state.students}/>
    </div>
  );
 }
}
```
We can take note of a few details:

* We have a `<form>`that contains a text `<input />` and a `<input type="submit" />` that functions as our submit button.
* On our form we have listed an `onSubmit` property and given it a value of `{this.handleSubmit}`. We won't go into crazy detail here as this will be explained in more detail in coming lessons. But just take note that it is happening.
* On our `<input type="text" />` we have an `onChange=` property that has a value of `{this.handleName}` and we've given the input itself a value of `value={this.state.name}`.
* We need that value from the input, because that is how we will grab the name that the teacher types into the input.

Now let's look at the methods we called on our `<App />` component. We defined where these methods would be used in our return statement we just examined, but now let's check out where we define what they do!

```js
export default class App extends Component {
  constructor(props){
    super(props);

    this.handleName = this.handleName.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);

    this.state = {
      students: [],
      name: " ",
    };
  }
  handleName(e){
    this.setState({name: e.target.value});

  }
  handleSubmit(e) {
    e.preventDefault();
    this.state.students.push({studentName: this.state.name});
    this.setState({students: this.state.students, name: " "});

  }

```

So here is what we need to take away from this portion of our `<App />` component:
* We have a `constructor(props)` with `super(props)` called inside of it. By now this should be familiar as all components created as a `class` should have a base constructor that receives props.
* We then see two funky expressions. `this.handleName = this.handleName.bind(this);` and `this.handleSubmit = this.handleSubmit.bind(this);`. We will examine this philosophy in the next lesson, but right now just understand that we are giving the two methods access to `this`.
* Then we see the initial state being set within the constructor:

```js
this.state = {
  students: [],
  name: " ",
};
```
* That simply lets the component know what changes it needs to keep track of. In this case, we want it to track an empty array called "students" and a variable called "name" that is set to an empty string initially.
* We then take a look at our methods `handleSubmit` and `handleName`:
* Inside of `handleName` we pass an argument `e` that is our `event` object. The onChange property listens for changes to the value of the `<input />` and fires each time a key stroke is registered.
* We then take the `e.target.value` which gives us the value correlated to our input and store it in the `state` of "name" : like so, `this.setState({name: e.target.value});`.
* This simply updates our state which can be retrieved throughout our component at any time.
* We move down to the next method, `handleSubmit`, and see that we again pass it an `event` object using the shorthand `e`.
* This allows us to call the `e.preventDefault()` method which prevents the form from trying to POST to the server.
* Next, we grab the current (state) value of our `name` and `push` that value into our `students` array:

```js
this.state.students.push({studentName: this.state.name});
```

We pass the array an object with the property `studentName` and the value `this.state.name`. This ensures that each time we hit submit, a new name will be added to our array.

* After that, we update the state using `setState` to make sure we have saved our changes:

```js
this.setState({students: this.state.students, name: ""});
```

* We also update the value of our `name` state back to an empty string (this clears our input box, since it's value is the value of `this.state.name`).

The entirety of the above Component is concerned with handling and updating the state of the student list. Now let's check out how we get that list to render on our application.

### Pass the props!
Inside of our `return` statement:

```js
return (
  <div className="class-maker">
    <h3>Create Your Class List Here: </h3>
    <form onSubmit={this.handleSubmit}>
      <input type="text" onChange={this.handleName} value={this.state.name}/>
      <input type="submit" value="Add Student" />
    </form>
    <StudentList students={this.state.students}/>
  </div>
);
```

We placed our `<StudentList />` component. This component was given a property `students` and passed the value of `this.state.students`.
This gives access of the state properties to `<StudentList />` component in the form of `props`.

Now let's peek inside fo our `<StudentList />` component and see what makes it tick and how it works...

```js
class StudentList extends Component {
  constructor(props){
    super(props);

  }
  render(){
    let kids = this.props.students.map((student, index) => {
      return (
        <li key={index}>{student.studentName}</li>
      )
    })
    return(
      <div>
        <h4>My Class:</h4>
        <ul>
          {kids}
        </ul>
      </div>
    );
  }
}
```

What to note:
* We are sure to pass the `constructor()` and `super()` with props to the component.
* Inside of our render method, we declare a variable using the ES2015 `let` syntax: `let kids =`.
* We set the value of that to :

```js
this.props.students.map((student, index) => {
  return (
    <li key={index}>{student.studentName}</li>
  )
})
```
* What happens inside of that is that we `map` over `this.props.students` (which was passed down from the `<App />` components in the form of `this.state.students`).
* We extract each student from that array and return an index and student as a list item :
`<li key={index}>{student.studentName}</li>`.
* The `student.studentName` give us access to the `studentName` property inside of our `students` array.
* We know that each mapped item needs a unique key, so we use the index of each item being mapped over for simplicity sake. `key={index}`.
* We then insert each mapping using bracket notation with `{kids}`. That is put into the `return` statement where the `<ul> {kids} </ul>` is placed.

And that is it! We have successfully taken data from a parent component and shared it down to a child component using `props`.

### Conclusion
* `props` allow for the transfer of data, while protecting the state and management of state in the parent component.
* We also took a look at setting the `state` (`this.setState({})`),  and how we can keep track of data within a component by using `state`.
* We looked breifly at binding `this` to the component's methods (`this.handleSubmit = this.handleSubmit.bind(this)`) which gave us access to `this` for the component.
* We checked out how `e.target.value` (or `event.target.value`) can be used to scoop up the values for inputs and then stored in the state to use later.
* We visited the `event.preventDefault()` method to stop our form from trying to post to a server.

#### References
[React Docs](https://facebook.github.io/react/docs/state-and-lifecycle.html)
