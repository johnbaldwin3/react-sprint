## The Redux Saga...
One of the main topics we have yet to hit on is a pretty important part of our Redux workflow. If you'll recall from a few lessons back when we first were introduced to our good friend redux, we spent some time talking about the cycle of data and the workflow of our application. We even had a nifty little diagram that showed how the cycle worked. Don't remember because you've been cramming so much information into your heads? Have no fear, we will show it again right now.

So here is what we went over previously:

![react-redux-workflow](./react-redux-workflow1.jpg)

We watched the user create some event that triggered our action creator to pass its action to our dispatcher inside of our store. The dispatcher then delegated the action to the reducers, and the matching reducer then created a new updated state depending on what the action needed. Pretty simple, hopefully!

Well, there is more to the puzzle than we led on at first. In Redux we have the ability to create functions that can do things for us in workflow cycle. Introducing, new to the show, Middleware.

### I've heard of the Middle of Nowhere, but what is Middleware?

As simply defined as possible, middleware provides a docking point for third party libraries and code. At the dock they can do something for us and then ship the action out to the reducer. Middleware can be used for logging things, crash reports, talking to/fetching from APIs, routing, and more! A key concept here is that we can use it for asynchronous events (like fetching data) --> that will come in handy in the near future.

So, quick recap, middleware basically intercepts the action from dispatch, does some stuff that we want it to, and sends it off to the reducers. That's the cycle.


### With that in mind...
With the newfound knowledge (albeit very basic) of middleware, let's look at revising our workflow! We've updated our little diagram to reflect middleware and where it fits into the puzzle of Redux (and React).

![redux-saga-workflow](./redux-saga-workflow.png)


#### [Child-Subsection Title]
[Content for each child-subsection subject in an objective.]
### Conclusion
[Summary of content covered]
#### References
[Resource links]
