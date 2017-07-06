## Stateless Components

State is not a required thing in React components. You can actually have components that rely only on the props. If you are not going to have any data that changes in the component, then there is no need for state - simply use props to pass static data.

### Component Types

//There are three different component types: Stateless, Stateless Functional, and Stateful//

**Stateless Component** — Only props, no state. There's not much going on besides the render() function and all their logic revolves around the props they receive. This makes them very easy to follow (and test for that matter). We sometimes call these *dumb components*.
Stateless components are pure functions of their props. They do not have lifecycle methods and do not retain internal state. Another way to think about it is that stateless components deal with the UI rather than behavior. This is why you'll also see them called *presentational components*.

```js
class List extends Component {
  render() {
  return (
    <div>
      <h3>Favorite Movie List: </h3>
      <ul className="list-group">
        {this.props.movies.map((movie, index)=>{
          return (
            <li className="list-group-item" key={movie.title}>
            <h3>{movie.title}</h3>
            </li>
          )
        })}
      </ul>
    </div>
    );
  }
}
```

**Stateless Functional Component** - If your component only has a render method, you can write it as stateless functional component, and your function will be passed `props` as its first argument like so:

```js
const List = ({movies}) => {
  return (
    <div>
      <h3>Favorite Movie List: </h3>
      <ul className="list-group">
        {movies.map((movie, index)=>{
          return (
            <li className="list-group-item" key={movie.title}>
            <h3>{movie.title}</h3>
            </li>
          )
        })}
      </ul>
    </div>
    );
  }
}
```

Another thing to note with the *stateless functional component* above is that you don't have any `this`, and you don't have to do any binding.

**Stateful Component** — Both props and state. We also call these state managers. They are in charge of client-server communication, processing data and responding to user events. We sometimes call these *smart components*. These sort of logistics should be encapsulated in a moderate number of Stateful Components, while all visualization and formatting logic should move downstream into as many Stateless Components as possible.

You've seen (and written by now) stateful components. Imagine if you wanted to let the user interact by inputting their favorite movies. Here's an example to compare to the stateless components we looked at above:

```js
export default class List extends Component {
  constructor(props){
    super(props);

    this.handleMovie = this.handleMovie.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);

    this.state = {
      movies: [],
      title: "",
    };
  }
  handleMovie(e){
    this.setState({title: e.target.value});

  }
  handleSubmit(e) {
    e.preventDefault();
    this.state.movies.push({movieTitle: this.state.title});
    this.setState({movie: this.state.movies, title: ""});

  }
  render() {
    return (
      <div className="movie-list">
        <h3>Favorite Movie List: </h3>
        <form onSubmit={this.handleSubmit}>
          <input type="text" onChange={this.handleMovie} value={this.state.title}/>
          <input type="submit" value="Add Movie" />
        </form>
        <MovieList movie={this.state.movies}/>
      </div>
    );
  }
}
```

#### To Have or Not Have State?

**Should this Component have state?**

*State* is optional. Since state increases complexity and reduces predictability, a Component without state is preferable. Even though you clearly can't do without state in an interactive app, you should avoid having too many Stateful Components. Optimally, your app would be comprised of mostly stateless components.

Often, apps are organized with higher level "container" components that manage state with multiple stateless components.

### Conclusion

- Stateless/dumb/presentational components deal with props only, do not have state or lifecycle methods
- Stateful/smart components manage state and props, and deal with processing data that is changing over time.
- Best practice in order to write clean code is to have mostly stateless components and a few stateful components. Choose wisely.

#### References

[JSPlayground](http://javascriptplayground.com/blog/2017/03/functional-stateless-components-react/)
[Todd Motto](https://toddmotto.com/stateful-stateless-components)
[Dan Abramov](https://medium.com/@dan_abramov/react-components-elements-and-instances-90800811f8ca)
