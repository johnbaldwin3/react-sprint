## The Benefits of Server Rendering

We touched on the basics of why Universal JavaScript is beneficial to our code and application, but let's take a few minutes to explore this in more depth.

### If you ain't first, you're last...

![aintfirst.gif](https://tiy-learn-content.s3.amazonaws.com/2c7e880b-aintfirst.gif)

In the infamous words of one Ricky Bobby... "If you ain't first, you're last..." - speed and perception of speed are everything in the world of web applications and web pages. Large companies such as Amazon and Walmart have done numerous studies on the efficiency of a web application and the relation of user experience and sales.

It should probably come as no surprise in this day and age that people want to get things moving, and quickly. Websites that take too long to load are left in the dust, literally people will not even wait to see the content if they don't load immediately.

#### Well, then how do we get to be first?
Universal JavaScript has a few main pillars, but one of them is that our initial load should come from server side rendering. That is to say our backend server, usually running Node or Express to be a Universal application, loads the initial page as quickly as possible. It then loads the rest of the page, piece by piece, allowing the user to begin exploring the website even before it is functional.

Of course the drawbacks are that some of the page will not respond to user events until the whole thing has loaded, but it gives the user the eye candy needed to wait it out.

Let's take a look at a diagram of how this works...

![ServerSideRendering.png](https://tiy-learn-content.s3.amazonaws.com/4d709f66-ServerSideRendering.png)

As you can see, we almost immediately have a page up and viewable, while the rest of our application finishes loading. This is really the key for success in web applications today - to satiate the users need for immediate results.

#### What's the difference.

No good example can be made without showing an example of the other option or opposite. Let's take a look at client side rendering, where all of our application loading from the client side of things, meaning it has to be pushed first to the server and then go through the motion of loading the entire application before it is both viewable and interactive. Let's see an example of that for comparison:

![clientsiderender.png](https://tiy-learn-content.s3.amazonaws.com/d6359d43-clientsiderender.png)

### Conclusion
* Universal JS helps us set up our application to be more efficient for our users.
* Using server side rendering allows our page to load almost immediately, giving the user something to look at it quickly.
* Being able to display a page more quickly has been proven to promote a better user experience.
* By using server side rendering, the page loads viewable material first, then continues loading the JavaScript files to make the page interactive afterwards.
* In comparison, client side rendering, loads the entire viewable and interactive content at the same time, which can slow down the load time and the time with which the user can even see content.

#### References
* [Walmart Labs Engineering](https://medium.com/walmartlabs/the-benefits-of-server-side-rendering-over-client-side-rendering-5d07ff2cefe8)
* [Smashing Magazine](https://www.smashingmagazine.com/2016/03/server-side-rendering-react-node-express/)
