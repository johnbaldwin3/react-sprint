## Application State... of the Union.

We have examined component level state in our journey through React Land. We know that each component has access to state if we want it to, and it can help manage the state of the application by passing around props to children components. We also know that managing state for all of the different pieces of data in our application is a tiresome event and must be carefully done so as not to "cross wires" in our components or needlessly meddle in state when it's unnecessary to do so. If only there was a tool to keep track of all of our state in one place...

...First stop in our story: Flux.

Flux library is an "application architecture" that was designed for this purpose and is used by Facebook and compliments React.js and its methods for creating views depending upon the data of the application. We won't go much further into Flux, but it is important to understand that what we are about to introduce was evolved from Flux and what Flux brought to the table.

Everyone, meet Redux. Redux, everyone. As mentioned already, Redux evolves the ideas of Flux, but is substantially less complicated once an overall understanding has been reached as to what Redux actually does for us. To understand Redux, we must first understand Application State.  


### Application Level State
When we refer to Application State or Application Level State refers to the entire data of the application. It has nothing to do with state that is on the component level, but in contrast it has everything to do with the data that flows through the entire program. The real magic of Redux is how it handles all of that data, the Application State, and manages what actions should be taken depending on what goes on in the application.  

#### What does that do for us?
By managing all of the application state for our app, we don't have to search all over and figure out which component is responsible for which piece of data - instead we can simply plug application state in to the components as we build our application so only the relevant components receive the state and the rest remain unaffected and unburdened with with the duty of managing state. When we develope our application we can ask ourselves a few questions to determine whether something should be handled by component level state or application state with Redux.

1. Do other parts of the application care about the data in question?
1. Do we need to create more data based on the data in question?
1. Is the data in question being used to create/drive multiple components?
1. Would there be value in having a record of the changes to state as you move through your application? (i.e. Would this help you debug your application if you could manage and track the changes past and present as you test your application?).
1. Do you want to cache (hold on to) your data instead of using multiple requests from another API?

If you answer yes to these questions, then it's time to start looking at Redux and how we can put it to use for us.


### Conclusion
* As our projects get more complex and begin to handle more data, there are tools we can use to manage our application state.
* Flux was designed to manage application state.
* Redux is a library that evolved from Flux and help us manage application state in a simple and straight forward way.

#### References
* [Redux JS: Organizing State](http://redux.js.org/docs/faq/OrganizingState.html)
* [Flux](https://facebook.github.io/flux/)
* [Redux ReadME](http://redux.js.org/)
