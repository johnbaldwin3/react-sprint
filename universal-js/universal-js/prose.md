## Universal JS and Isomorphic JS

With advancement in the way applications are created and optimizing how fast we can run them on the internet, we have developed new and exciting possibilities to make our apps as efficient as possible. We are going to discuss Universal JavaScript and Isomorphic Javascript in a compare and contrast sense to examine what these two widely used terms means.

### In the beginning, there was Isomporhism.

Ancient Greece is credited with creating the word isomorphism. It stems from the Greek word "isos" which means *same* and the word "morphe" which means *shape*. It was used to describe an overall scientific theory that if something was truly a consistent shape, it would be the same no matter the context in which it was viewed.

Kinda complicated - especially when you get into the rabbit holes of chemistry and dealing with elements, but we are not going to do that. What we do need to take away is that we are going to have *two different ways* to view/use the *same thing*.

In programming, being isomorphic relates have a server side code and a client/user side code both working together to render our application on the web without losing the state or power of the application - and furthermore, increasing its efficiency.

Isomorphism on a general level is being able to render something on multiple platforms, across different languages. However, we are going to stick with JavaScript.. so we will be referring to Isomorphic (JavaScript) JS.

### So what is Universal JS?
Well the line is muddied between the two terms. There are camps that side with using Isomorphic JS over Universal JS and vice versa. For our purposes they are essentially the same. Especially when tagging the JS (JavaScript) to the end of the word.

That being said, when we say Universal JS, we are referring to a specific code that we have written in JavaScript which is able to run in multiple environments. Both the client/user side of the application and the server side of the application. Most commonly this splitting of code between the two environments is between client side JavaScript libraries (such as React in our case) and server side JavaScript such as Node.js.


#### Now that we know, why?
Well, there are some very complex answers as to why we would want to do this, but the most simple is efficiency. The larger and more complex our application get, the longer the load times and worse the experience for the user gets. One of the principals of Universal JS is to have a main page of the application that allows for instant user interaction while loading the remaining portions of the application and all of it's libraries.

JavaScript is really one of the only languages that can safely run on either platform without being bogged down. It is said to be agnostic of it's environment - meaning it doesn't care where it is run (server or client side). This ability means we don't have write code twice. The browser can interpret JavaScript from both the server (Node.js) and the client (React.js) without much trouble.

#### Forget everything I said...Well some of it...

A parting gift: Isomorphism and Universal JS are two different things, but they are tied together. There *really is no such thing as Isomorphic JS - there are only Isomorphic applications. All Universal JavaScript application are isomorphic applications*. The term Universal is just a cute word that is trending with the times, but honestly isn't needed - because we know JavaScript to be agnostic already. The benefit from using the term comes from the mindset of developing our applications with run time / production end results in mind.

### Conclusion
* Isomorphic JS is really the term Isomorphism.
* Isomorphism refers to an application that can be run in multiple environments (server and client).
* Universal JS is a term that describes a JavaScrip application that is isomorphic in its nature.
* Commonly Universal JS apps are written in Node and regular front end JavaScript. (In our case using React which works very well with server side JavaScript).

#### References
* [Gert Hengeveld's Medium Blog](https://medium.com/@ghengeveld/isomorphism-vs-universal-javascript-4b47fb481beb)
