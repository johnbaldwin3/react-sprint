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
For the sake of keeping it simple and trying to grasp what's happening 

### Conclusion
[Summary of content covered]
#### References
[Resource links]
