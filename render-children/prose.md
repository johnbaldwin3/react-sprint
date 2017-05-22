## Rendering Child Components in React
Inheritance in React can be a tricky thing. Considering the way React builds things, some components may not even be aware of the children components they will have later on. How do we tackle this problem? Let's take a look...

### Consider a BaseLayout Component
Let's think for a minute that we have a component that consists of our Navigation Bar and our Footer that we would like rendered on almost every page.

```js
class BaseLayout extends Component {
  constructor(props) {
    super(props);
  }
  render() {
    return(
      <div>
        <nav>some stuff here</nav>

        <footer>some more stuff here</footer>
      </div>
    );
  }
}

```

This is a very simplistic view, but let's think about what is going on here. We've got a main div that holds both our navigation and footer elements (which most certainly could be components on their own as well).

What if, at the same time, in our main App.js file we had something along the lines of this...?

```js
class App extends Component {
  render(){
    return (
      <BaseLayout>

      </BaseLayout>
    )
  }
}
```

How would `<BaseLayout></BaseLayout>` be able to render any other components that needed to go between the navigation and footer elements inside of it?

#### Use props.children !
In order to pass components into another component that may not know what it's children are going to be, or may render many different children depending on the page, we use `{props.children}`
### Conclusion
[Summary of content covered]
#### References
[Resource links]
