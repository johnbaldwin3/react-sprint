## Hash-based Routing Drawbacks

In the previous lesson, you learned about hash-based routing. Let's use an analogy to think about how routing works. Imagine you want to read a book, so you go to the library. The book you want to read is like the web page you're visiting. You know the exact book you would like to read.
Here are 2 scenarios depending on which routing method you use:
1. You walk in and tell the librarian you would like to read something by H.P. Lovecraft. The librarian pulls up a cart with all 100,000 of his letters. Then the librarian asks you which title you would like to read. You tell them, and they pull out and hand you the book.
2. You walk in and tell the librarian the title of the book you would like to read. They grab that specific book and hand it to you.

In the first scenario, you are using hash-based routing. Using the hash, you first pull only the main url of the website (in the analogy - the cart of all things written by the author). Then after the server grabs this, some code is sent back and the browser then pulls the fragment identifier (specifying exactly which page you want) out of local storage and sends a query back to the server. Then the server returns the exact page matching the query.

The second scenario is resource routing. You send the full url with query string to the server and it fetches the exact resource you require.
They work in different ways, but both methods work.

Ahh but wait, there's a third scenario. Suppose in scenario 1, you go in and tell the librarian the name of the author you'd like to read. They come back with the cart, then ask you which title, but they say it in Swahili. You have no idea what they are saying. You tell them to speak English and they start yelling at you in Swahili and communication breaks down. Okay so maybe the server won't yell at you, but it will return an error code which will probably make you yell at the computer. This is what happens when the browser you are using is not running Javascript, and the code returned cannot be read. Which means you end up with a broken link. Not good...

### A little history

Once upon a time, there was no such thing as a search engine. Yes, it's hard to imagine life with Google, and yes, it was a hard life. Then, someone came up with the idea of 'crawling' urls to be able to search for things! Fast forward to 2011, when Gawker/Lifehacker redesigned their sites with hashbangs resulting in site-wide outages. You can read about it in detail [here](https://www.wired.com/2011/02/gawker-learns-the-hard-way-why-hash-bang-urls-are-evil/) but the gist is that the URL with the hashbang depends on JavaScript to retrieve the content, and when the JavaScript failed to load properly, every URL on their page was broken.

### Hash it out

You're now asking "why would you even use hash routing then??" The hash-bang was originally intended as a means to help search engines index dynamically loaded AJAX websites. It can help to speed up page loading time, as the browser will load the static html content of the base url once, and then download the dynamic content related to the fragments as they are requested. So if the bulk of your site is made up of static HTML, with dynamic content being a minor component, then this set-up would help your pages load faster.

So maybe hashes aren't the devil?

Don't get ahead of yourself. Turns out another issue with using hash-based routing is that the URL fragments don't appear in browser history. Foiled again!
The browser loads the page faster because it ignores URL fragments where the base URL is the same,  deciding to load the HTML from the cache. The side effect of this is that URLs that differ only in fragments will appear as one entry in browser history. This means the user can't hit the back button to navigate on your page. And they also can't bookmark a specific page that's pulled from a fragment.

### Conclusion

![Monty Python Newt Got Better Image](./mp-newt-got-better.jpg )

Fret not, it gets better. There are other ways of routing that we can use to give the best possible user experience. One such example we have already covered, using the HTML5 History API. Another way which we will cover in detail is the React Router.

#### References

[Broken Links](http://www.tbray.org/ongoing/When/201x/2011/02/09/Hash-Blecch)

[Breaking the Web with HashBangs](http://isolani.co.uk/blog/javascript/BreakingTheWebWithHashBangs)
