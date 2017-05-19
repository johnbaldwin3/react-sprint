## Using and Importing Partials with Sass

As you might have already noticed, Sass is definitely geared to making your life easier and more efficient when it comes to styling and stylesheets. If you've created any sort of complicated design based website or application, like a pixel perfect rendition of something, then you know how long a stylesheet can get. We can be talking about hundreds of lines of code for just the styling alone.

In JavaScript we are able to break up our files into multiple files to make them more manageable and to help keep track of certain pieces of code that you may want to reuse or easily change. Well, Sass gives us that awesome ability also through the use of *partials* and *imports*.

### What are partials?

Partials are Sass files that contain smaller pieces of code that you can import into other Sass files. The ability to do this leads to more organized and efficient code, which means easier to maintain, which means more time to do other stuff! A partial file in Sass is a file that starts with an underscore. Let's call ours `_coolPartial.scss`. They can be named anything so long as there is an underscore leading the way. The underscore tells the compiler that the file does not need to be generated as its own CSS file (which we should only need one of!).

#### Our Partial File

For the sake of learning, let's keep it simple. Our file `_coolPartial.scss` is going to house a tiny bit of code to make some changes to a div with an id of `#tigerPaw` in our HTML. This is probably not how you would encounter a partial, but it will help illustrate exactly what is happening.

```CSS
/******* _coolPartial.scss file ***/
#tigerPaw {
  background-color: white;
  color: #F66733;
}

```

#### Importing our Partial

"Hey, Beam me up Scotty" - to import our `_coolPartial.scss` file into our `main.scss` file, it's quite simple. We just need to include an `@import` statement at the top of our main file. Let's check that out --->

```css
/******** main.scss file *********/
@import 'coolPartial';

/***** rest of styling codes would be below ***/
```

So all we did was use the `@import` followed by the filename minus the `_` and the `.scss` (in the case above `coolPartial`) in quotes. As long as the other style sheet is in the same directory sass just needs to know what the file is called and it can do the rest. Thanks Sass, you're the best!


### Conclusion
* The ability to create partials allows us to modularize our styling code into specific pieces and helps us organize our file structure.
* To create a partial, simply go in the same folder as your main `.scss` sheet and create a file using the underscore as a starter. i.e. (`_coolPartial.scss`).
* To gain access to that file in another file, just use an `@import` statement that calls on the filename without the leading underscore or the trailing filename. i.e. (`@import 'coolPartial'`).

#### References
[Sass Partials](http://sass-lang.com/guide)
