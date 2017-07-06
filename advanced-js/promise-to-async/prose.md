## Promise me! I've got an Async-ing feeling about this.

We've taken a look at how async/await functions work on a basic level. Let's dive a little bit deeper in to their use, most specifically their use in converting Promise functions for us.

We can essentially replace the Promise function altogether (though it is still wrapped up neatly for us behind the scenes) and use async and await to handle the whole "shabang".

### Promise me this - you'll reach for the stars...
Our first step in the land of converting to async will be to take a look at a very generic promise function and then invoking it in another function that will require us to manage promises.

```js

//creating a naturally asynchronous function
//depends on the server for it's completion, so we can not guarantee when it will finish
function getStarWarsStuff(url) {
  //we return a new Promise function (with a resolve and reject set of arguments)
  return new Promise((resolve, reject) => {
    //create an http GET request
    let theRequest = new XMLHttpRequest();
    //open our request with the url being passed in
    theRequest.open('GET', url);
    //when the request has loaded - we check the server response status...
    //if we get the 200 green light, then we retrieve the response data
    theRequest.onload = () => {
      if(theRequest.status == 200) {
        resolve(theRequest.response)
      } else {
        //if we don't get status of 200, we show the error.
        reject(Error(theRequest.statusText));
      }
    }
    //send the request through once we get properly set up with the above function
    theRequest.send();
  });
}

// create a new function that depends on the getStarWarsStuff function to run.
function starWarsify(url) {
  //call our function in the return statement.
  //use `.then` to wait for response to go through and then log Success and response...
  //or Failure and error message.
  return getStarWarsStuff(url).then(response => {
    console.log("Success", response);
  }, error => {
    console.log("Failure", error);
  });
}

//call the function with a url passed in and check our log for the results.
starWarsify('http://swapi.co/api/people/');
```

So, most importantly, that works. We can get the response back and sure we could definitely parse through and do a bunch of stuff with it, but we are trying to keep this as bare bones and simple as possible. So that is it - we created a promise function without async and await being used - the only thing left to do now is convert it to our new found knowledge of async/await functions and see how it differs.

#### Await the change...Lip-async-ing along with the tune..
Ok.. so.. let's convert it.

We will use the same exact `getStarWarsStuff` function and not change a thing there, but then rewrite a new function to run it using async and await:

```js
//same function as before...
function getStarWarsStuff(url) {
  return new Promise((resolve, reject) => {
    let theRequest = new XMLHttpRequest();
    theRequest.open('GET', url);
    theRequest.onload = () => {
      if(theRequest.status == 200) {
        resolve(theRequest.response)
      } else {
        reject(Error(theRequest.statusText));
      }
    }
    theRequest.send();
  });
}


//let's turn the previous function into an async / await function now that doesn't depend on a lot of "then" functions.
async function starWarsification(url) {
  //use await to wait for the async getStarWarsStuff to finish
  let stuffWeWantToGet = await getStarWarsStuff(url);
  //log the response;
  console.log("STUFF WE WANT!", stuffWeWantToGet);
  //return the value for use if needed...
  return stuffWeWantToGet;
}
//run it
starWarsification('http://swapi.co/api/people/');
```

A lot less code and more compact coding is achieved using the async and await functionality. We have now successfully converted our promised based function to run with async and await!!! Cool!!

### Conclusion
* Promise based functions can be converted to run as async functions.
* We can get rid of `then` chains using `await` instead.
* Converting these promised based functions helps minimize our code and use DRY programming.

#### References
* [Joel Zimmerman, Nilson Jacques Article](https://www.sitepoint.com/simplifying-asynchronous-coding-async-functions/)
* [Promises, MDN](https://developers.google.com/web/fundamentals/getting-started/primers/promises)
* [David Walsh - Promises](https://davidwalsh.name/promises)
