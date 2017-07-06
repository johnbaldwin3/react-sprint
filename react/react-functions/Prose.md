## Binding functions in React

We've talked about the `this` keyword a few times, and it's generally agreed that it is pretty confusing. Let's try to break it down so we have a decent understanding. Remember that functions are special objects. Just as functions can be passed around like objects, they can also be bound to the component and passed down as properties. For instance, when we made our form, we wrote an event handler and bound it to the component.

### Why does it have to be so confusing!?

In Javascript `this` functions differently in different scenarios. Let's review.

In a constructor, you use the `new` keyword to create a new object. In that case, `this` always refers to the new object being constructed. And we talked about the reasons to use strict mode, as otherwise `this` gets set to the global object `window`. When a function is defined as a property of an object, it is called a method. In those cases, you can use `this` to bind properties to their parent component. The confusion comes up because unlike regular variables, the `this` keyword does not have a scope, meaning nested function do not inherit the `this` value of their parent function automatically. Specifically, when you invoke a method inside of another function or component, the `this` value for that method is set to the object it was invoked upon, not the object it was invoked inside of...

We dealt with this previously when we created event handlers. We had to add a line of code in the constructor function to bind the `this` in the event handler to the `this` of the parent component.

Is your head spinning? Let's look at an example similar to one you've seen before, to see it in practice:

```js
export default class List extends Component {
  constructor(props){
    super(props);

    this.handleTopping = this.handleTopping.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);

    this.state = {
      pizza: [],
      topping: "",
    };
  }
  handleTopping(e){
    this.setState({topping: e.target.value});

  }
  handleSubmit(e) {
    e.preventDefault();
    this.state.pizza.push({pizzaTopping: this.state.name});
    this.setState({pizza: this.state.pizza, topping: ""});

  }
  render() {
    return (
      <div className="pizza-maker">
        <h3>Favorite Pizza Toppings List: </h3>
        <form onSubmit={this.handleSubmit}>
          <input type="text" onChange={this.handleTopping} value={this.state.topping}/>
          <input type="submit" value="Add Topping" />
        </form>
        <ToppingsList pizza={this.state.pizza}/>
      </div>
    );
  }
}

```

In the above example, we are allowing the user to input their favorite toppings for pizza. We created an event handler to handle the user input of toppings called `handleTopping`. We invoke that handler on `this` inside the `render` method using the `onChange` function. But we actually want the `this` context to come from the top level component. This is important because we want that handler (method) to have access to the properties, state and methods of the component. So to ensure `this` is bound to the correct context, we explicitly write a line of code in the constructor method to bind our event handler to the `this` of the component: `this.handleTopping = this.handleTopping.bind(this);`  

### More than one solution

There's more than one way to rescue a cat. The above is the recommended way to bind your functions to a component, however there are some other options that will work. Two different but similar methods both bind the function directly in the render. Looks something like this:

```js
<input type="text" onChange={this.handleTopping.bind(this)} value={this.state.topping}/>
```

Or using an arrow function:

```js
onChange={e => this.handleTopping(e)}
```

The issue with both solutions above is that you may run into performance issues since the function is reallocated on every render. So these solutions are not optimal.

While the first solution we went over is the one currently recommended in the React docs, there is a new technique that is a little more elegant and makes for cleaner code. This solution involves using class properties and the arrow function.

```js
handleTopping = (e) => {
  this.setState({topping: e.target.value})
}
```

By writing the code this way, you're taking a method and turning it into an expression. And by using the arrow function syntax you're gaining access to the `this` property of the component, saving you from needing to use the bind method. However, while this is available in ES6 (ECMAScript 2015), it is in the experimental stage and may be removed in later iterations. So, you may want to hold off on this solution until/unless it becomes more widespread.


### Conclusion

`This` is not always what we think it is. Especially when we invoke a function inside a method. In order to make sure `this` is bound to the right context in React components, we explicitly bind it in the constructor method. There is more than one solution to this issue, but binding in the constructor method is the recommended solution.

#### References

[Todd Motto](https://toddmotto.com/understanding-the-this-keyword-in-javascript/)

[GitHub Gist](https://gist.github.com/amitai10/adb66d6faa714e8c3cdb94946bb98356)
