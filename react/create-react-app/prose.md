## Getting Started with React!

Getting started creating a React application is not too difficult using the `create-react-app` library from npm. We will take a look at how to get create-react-app installed and begin an application using create-react-app. After we get up an running with an application, we will examine the React application itself and some of the basic philosophy behind React, how it is use, and what it is used for. We will also take a look at a new language, JSX, that is commonly incorporated by most React applications to take the place of HTML.

### Installing 'create-react-app' from npm.
Create-react-app is a library that helps us build React projects. It contains all of the goodies that will take our React application and translate it into something the browser can understand. It also provides us with a development server (which simply is a place we can watch our app from as we build it, without having to post it to a real server on a website). It will also, and most obviously, include all of the React libraries we need to make an application in... you guessed it... React!

#### So how do we install 'create-react-app' ?
It is likely that you will create more than one application with React, hopefully if you have chosen this path to become a React developer, then it is only the beginning of many projects. Sure there are tons of different ways to create React applications and means of installing the dependancies to do so, but let's look at a very simple and thorough means using 'create-react-app' and how to install it "globally" so that we need not install it over and over again every time we want to make a new React app.

The first step is to open up our terminal. It will not matter the directory we are in just yet, since we will be installing globally. On your command line, enter the following code:

```
npm install -g create-react-app
```

It will take a second to download all the tools and included goodies, but overall, that's it! We're ready to React!


### Beginning an application using 'create-react-app'
Okay, we've got the goods, but what do we do with 'em?

* The first step, **make sure you are now in your directory where you keep all of your projects**.
* There is no need to create a project folder, 'create-react-app' will do that for you, which is why we want to double check that we are in the directory that we want to create a project folder inside of.
* Once we are sure that we are in the right place, we can use the following command to initiate and create a React application.

```
create-react-app the-name-of-my-application-here
```

*Just to clarify, after we type 'create-react-app', we provide a space, and the name of the folder that we wish our application to be created inside of.*

* After this builds, we must actually open our project folder. We do so with the following code:

```
cd the-name-of-my-application-here
```

* Once inside, we can open our project using our code editor, if using ATOM, the following would open our application. (Be sure you are inside of your project folder)

```
atom .
```

Once atom opens up, you will see the layout of what was installed in your project folder. It should look something like this:

```
my-app/
  README.md
  node_modules/
  package.json
  .gitignore
  public/
    favicon.ico
    index.html
  src/
    App.css
    App.js
    App.test.js
    index.css
    index.js
    logo.svg
```


#### Opening up the dev server... (development server).
We can now also open up our development server. The development server will track changes as we create our application. Each time our application is saved, the development server will automatically update in the browser for us and show us our changes.

To get the development server up and running we need to type the following command in the project folder:

```
npm start
```

* It should automatically open up a browser window with your project ready to go and watching for changes. If it doesn't open automatically however, you can enter the following address in your browser "http://localhost:3000".
That's it, it's time to become a React developer... let's check out how we do that with some baby steps first.

### Why do we use React?
Because it's awesome! That's why.

React is awesome and amazing, but why exactly did we choose React? React is on the frontline of development for front end engineering of software. How did it get there? Well you can certainly visit the React page to learn the history, but we want to examine what makes it special. React specializes in managing the data in an application and updating the application when changes occur. It does this without the need to use a refresh or reload button and constantly monitors the application for changes for us.

#### Monitoring the changes...
Without confusing everyone on the first look at React, we will keep this explanation simplified for the first run-through. In basic terms, React creates what is known as the "Virtual DOM". You should be familiar with the "DOM" by now, but that is our "Document Object Model". The Virtual DOM is really just a fancy way to say a "copy of the DOM". React works by constantly comparing the copy of the DOM to the actual DOM of our application. When React sees changes - it automatically re-renders the application for us. Data being received, data being given by a user, various animations, etc... all of these by the nature of what they are change the DOM. React listens and renders the application accordingly.

### Translating HTML into JSX
So we have a very high-altitude overview of what React does, but how do we React? React works as a "SPA", or "Single Page Application". Most common practice uses an HTML page with one `<div id="root"></div>` inside the body of the HTML document. That <div> is the source for the entire application. That's really all of the HTML you are going to need to write... SAY WHAT!?

Yes, you heard it correctly. The rest of our project is going to be made up of components and JavaScript. The components are written in the language of "JSX", which is "XML" syntax combined with JavaScript. It should be noted that you can most certainly use pure JavaScript to create components, but most developers agree that JSX makes the project much more streamlined, elegant, and prevents us from directly incorporating pure HTML into our JavaScript files.

#### Super Cool App
For the sake of keeping it simple and trying to grasp what's happening we are going to create a less than awesome website that will have zero functionality at this point. What we will focus on is the translation of HTML into JavaScript and how we tackle getting started with our 'create-react-app' format. So let's first look at some less than stellar HTML below. This is the beginnings of an application that allows you to input your favorite Bill Murray movie and will display something about it depending on what the input was.

So here's the HTML, nothing fancy, just what you would expect to see on your "index.html" file... (also for keeping it short, we will just examine the body of the HTML document)

```HTML
<body>
    <nav class="navbar">
      <h1 class="title">Favorite Murray</h1>
    </nav>
    <main class="main-body">
      <div class="top">
        <div class="image-one">
          <img src="https://www.fillmurray.com/200/300" alt="Fill Murray Pictures">
        </div>
        <p class="top-paragraph">
          Lorem ipsum dolor sit amet, consectetur adipisicing.
        </p>
      </div>
      <div class="bottom">
        <div class="image-two">
          <img src="https://www.fillmurray.com/300/300" alt="Fill Murray Pictures">
        </div>
        <p class="bottom-paragraph">
          Lorem ipsum dolor sit amet, consectetur adipisicing.
        </p>
      </div>
    </main>
    <div class="murrayinator">
      <h3>What's your favorite Murray Movie?</h3>
      <form class="murray-form" action="" method="">
        <label for="murray-movie">Type your favorite movie here...</label>
        <input type="text" id="murray-movie">
        <button>Submit</button>
      </form>
    </div>
    <div class="answer">
      <h4 class="murray-display"></h4>
    </div>
    <script src="js/bundle.js"></script>
  </body>
```

### A look at the 'create-react-app' set up and writing JSX
After our install, we have a set up structure as seen in the folder layout from earlier. We are primarily going to be concerned with 3 parts in order to create a React application. We will not be styling anything for this cool app, so the three documents we need to take a look at are:

1. public/index.html
1. src/index.js
1. src/App.js


#### public/index.html
This will be short and sweet... the only portion of concern for us with HTML moving forward is the `<div></div>` in which our application will be inserted. 'Create-react-app' has already provided us with some HTML to get started and given us the following <div>:

```HTML
<div id="root"></div>
```

That's really all we need to know about this page, we will not write anything else in this document, but just know this is where the magic happens.

#### src/index.js
This is our main JavaScript file. Inside of this page you will see very little written already by our 'create-react-app' set up. We will also not touch this page further, but let's examine what's going on here.

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import registerServiceWorker from './registerServiceWorker';
import './index.css';

ReactDOM.render(<App />, document.getElementById('root'));
registerServiceWorker();
```

There 5 `import` statements at the top of this page, we are only going to discuss three of them for now.

The first thing we are doing is importing React into our project (makes sense, right?). The next thing we import is "ReactDOM". ReactDOM is the glue that holds our React project and the DOM together. We use the ReactDOM to render our application and tell it where to insert itself in the DOM.

In our ReactDOM statement above you can see that we call :

```js
ReactDOM.render(<App />, document.getElementById('root'));
```

This is essentially saying we want to use our `<App />` and insert it into the HTML page at the element with an ID of `root`. We already looked at our HTML and saw the `<div id="root">` tag in the body of that document. ReactDOM will render that `<App />` tag inside of that `<div>`.

The last piece is the importing of our App, from the 'src/App.js' file. This allows us to call it inside of the index.js and render it using ReactDOM.

#### src/App.js

The final piece of the puzzle is the App.js file. This is where the beginnings of the magical world of React will take place for us. Our App.js file has been set up with a bit of stuff already included - so let's examine that and see what we need and what we will have to change to get started.

```js
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <div className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h2>Welcome to React</h2>
        </div>
        <p className="App-intro">
          To get started, edit <code>src/App.js</code> and save to reload.
        </p>
      </div>
    );
  }
}

export default App;

```

We are familiar with classes and extending, as well as importing, so none of this should be too weird, but let's break it down so we can get started.

At the top we import React, and the Component library from React in the first statement `import React, { Component } from 'react';`. We also import a logo, that we don't care about at this point, as well as our style sheet, which we are not concerned with either.

The first thing we have is a `class` called `App` that extends (inherits) from the React.Component library. We call a render method on that component, and return some funky looking stuff called JSX.

* One of the big things with these return statements is that a component can only render one div, or piece of JSX. Everything must be contained within that one div. Therefore something along the lines of

```js
return (
  <div></div>
  <div></div>
)
```

**Would be invalid!!!** It all needs to be in one container.

For what we are after, we can go ahead and delete everything so we are left with the following:

```js
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">

      </div>
    );
  }
}

export default App;

```

Since we are writing in JavaScript (JSX), reserved words such as `class` can not be used, so if we want to give a class name to our JSX tags, they must be camelCased into `className`.

In general any HTML attributes will be camelCased in JSX.

The HTML `for` attribute is also a reserved word in JavaScript, so it becomes `htmlFor`.

Also, any normally single line tags, such as `<img >` and `<input >` must become self closing tags in JSX. In fact all tags must have a closing tag or be self closing. The two examples above would now be written as `<img />` and `<input />`. Also, if you think back to our index.js file, you would notice that our `<App />` tag was self closing too!

So, now let's see what our app would like in JSX:

```js
class App extends Component {
  render() {
    return (
      <div className="App">
        <nav className="navbar">
          <h1 className="title">Favorite Murray</h1>
        </nav>
        <main className="main-body">
          <div className="top">
            <div className="image-one">
              <img src="https://www.fillmurray.com/200/300" alt="Fill Murray Pictures" />
            </div>
            <p className="top-paragraph">
              Lorem ipsum dolor sit amet, consectetur adipisicing.
            </p>
          </div>
          <div className="bottom">
            <div className="image-two">
              <img src="https://www.fillmurray.com/300/300" alt="Fill Murray Pictures" />
            </div>
            <p className="bottom-paragraph">
              Lorem ipsum dolor sit amet, consectetur adipisicing.
            </p>
          </div>
        </main>
        <div className="murrayinator">
          <h3>What is your favorite Murray Movie?</h3>
          <form className="murray-form" action="" method="">
            <label htmlFor="murray-movie">Type your favorite movie here...</label>
            <input type="text" id="murray-movie" />
            <button>Submit</button>
          </form>
        </div>
        <div className="answer">
          <h4 className="murray-display"></h4>
        </div>
      </div>
    );
  }
}

export default App;

```

There is plenty more to discuss about React, but for now, these are the basics to get a project up and running. By exporting our App and then importing into our index.js, we can see the power that React has to start making truly smart software that only renders on one HTML page.

### Conclusion
* 'create-react-app' is easily installed with the `npm install -g create-react-app` command.
* To get a project started, simply use the `create-react-app my-app-folder-name` command (naming the folder whatever you want for your project)
* After naming the folder, use the `cd my-app-folder-name` command to change into that directory.
* Use `npm start` to start up your development server to watch for changes and render your application to view while you work on it.
* React most commonly uses JSX language to take the place of HTML and all React components will be rendered in a singular <div> on your index.html page.
* JSX requires camelCasing and special words to take place for reserved words such as "`class`" and "`for`" in JavaScript. These examples would be replaced by "`className`" and "`htmlFor`".

#### References
[React Docs](https://facebook.github.io/react/docs/hello-world.html)
