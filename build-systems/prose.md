## What is a Build System, Why do We Use Them?
What is a build system? Why do we utilize them for front-end applications? Well it may or may not be a surprise to find out that we have already been using them. Our `create-react-app` is a form of build system. So let's take a look at what exactly a build system is and why it is something we use in front end development.

### What is a build system?
Because we don't want an egg before the chicken, we need to understand what a build system actually is in order to understand what it does.

To know a build system, we first must know workflow. Workflow is the set of tasks that someone goes through when doing a job. Every job has a different workflow and many jobs have more than one workflow. Web development is no different. All of the tasks required to create a web application have a series of steps that must be completed in order to get to a final production ready product.

A build system is a set of tools designed to make the workflow of web development easier. Build systems are composed of kind of a Jekyll and Hyde partnership of tools that work for us to make our lives easier.

#### Dr. Jekyll
The first area of build systems we are going to examine are what we can refer to as "installers". Installers do exactly what you might expect and install things. You've been using installers for some time now. *npm* (Node Package Manager) is a tool we employ in our bash terminal commands to install front end libraries and dependencies - such as React.js, React Router, or Sass. npm can also help us install servers to run our development environment on (`npm start`) so we can see our project as we work on it. npm can even help us install other installation tools! Other installers include Bower, Yeoman, and Brew.

#### Mr. Hyde
The other half of a build system we can refer to as the "doers". These additions perfom tasks for us and use their own special packages and plugins to complete the task. Things such as Babel, webpack, Require.js, Browserify, Gulp, etc. are all considered doers and help us to do various tasks for us. Babel for instance is a translator that can take JSX and translate it to regular JavaScript, or ES2015 syntax into ES5.

### Development vs. production
The end game for a build system is to get us ready for production, that is to send our code out into the wild world of the web and up and running on a server. Often times during our development of an application we can have tons of files and folders - this chaos would ultimately lead to slower loading and poor functionality of an application. Build systems are often responsible for minimizing file sizes and compacting folders into a much more streamlined and efficient version of our project, which enables it to run much more smoothly on a server.

### What build system tools do we use?
Well like much of development, that choice ultimately will land in your hands, or the company's hands you work for. There are a limitless combination of ways to set up build systems, but what it really boils down to is what you will need for your project size, style, and application.
[Content for each child-subsection subject in an objective.]


### Conclusion
* Build systems are designed to make our workflow easier and automate a bunch of tasks for us.
* Build systems are made up of two different types of tools:
  * Installers: like npm or Bower help us install libraries and dependancies like React.js, or Sass.
  * Doers: like Babel or webpack, help us complete specific tasks in our project by taking the workload off of our shoulders.
* A build system should be comprised of the right tools for your project, the right amount of installers and doers to get the work done.
* There countless variations and combinations to make up a build system, choose only what you need for your work.
#### References
* [radify.io: Using Build Tools](http://radify.io/blog/using-build-tools/)
