## Hash based routing vs resource routing

Routing simply means your app responds in some way to a change in the browser's URL. By now you are familiar with the client-server model: the web browser is a *client* program that requests a resource (web page) from the *server*. Resource routing refers to routing done on the back-end, for example with NodeJS. Hash-based routing is done on the front-end. Mmm yummy hash. No not that kind. We're talking about the hash symbol here #. But first, let's review what you know about resource routing.

### Resource routing

Resource routing essentially refers to back-end routing. You have done some of this already using NodeJS. You used the POST and GET request methods to communicate with the server. In resource routing, those methods send a request to the server, the server then searches for the resource you requested, and responds back with a static file that is stored on the server. Routing in this case is handled by the server or back-end.


### What is hash routing?

Hash based routing is a method of routing that uses the hash symbol to designate the path that the router should direct the browser onto. These symbols are placed after the base URL and before the route. `http://myrecipes.com/#/hashbrowncasserole` It essentially separates the URL and creates a fragment of the remaining piece of URL, called a fragment identifier. When the browser detects the # symbol, it ignores everything after that. The baseURL is sent to the server, while the fragment identifier is stored in local storage. The server processes that request for the base url and returns the default index.html. Then, some javascript is returned to the browser, the code is run, and a query is sent to the server with the fragment. This is then shown in the view for the user. (To be able to process the hash-bang URL, the browser it's being sent to needs to be using Javascript. We'll go into more detail about the issues this may cause in the next lesson.)

With the url example from above:

```js
http://myrecipes.com/#/hashbrowncasserole

// the base url myrecipes.com will be sent to the server, the fragment identifier /hashbrowncasserole will be stored in local storage. Javascript code is returned to the browser after the initial page is pulled, prompting the browser to then send back the fragment as a query to the server.
//
```

#### hash-bang

You may sometimes see the hash symbol followed by the exclamation mark: #! which is referred to as hash-bang or sometimes shebang. This was created to allow for ajax crawlable url strings, meaning search engines could find your content. However this has since been deprecated by Google, and it's recommended to use the History API.

### Conclusion

When you hear the terms resource routing and hash routing, you now know that they refer to back-end vs front-end routing methods. There are advantages and disadvantages to each which we will cover more fully in the next lesson.

#### References

[Basic resource routing](https://expressjs.com/en/starter/basic-routing.html)
[Client Server](https://en.wikipedia.org/wiki/Client%E2%80%93server_model)
[Simple summary front-end vs back-end routing](https://medium.com/@kennedyjt88/frontend-routing-vs-backend-routing-874b2bc41e5a)
