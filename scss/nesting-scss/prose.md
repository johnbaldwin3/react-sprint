## Nesting with Sass

This isn't for the birds! In CSS nesting of elements is not a thing. Each element needs a specific ID or a lot of code to drill down to the right element and not blanket all similar elements with the same style. Well with Sass, we can nest our elements and very efficiently save a lot of extra code while targeting precisely what we are after.

### Know the past to know the future

Let's pretend for a moment that we've got a navigation bar in our HTML. For the sake of simplicity this is going to be one very simple navigation bar.

```HTML
<nav>
  <div class="title">Title Bar</div>
  <ul>
    <li>Some Stuff</li>
  <ul>
  <a href="#">Link</a>
</nav>
```

In order to style this you might do something like the following on your stylesheet.

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav li {
  display: inline-block;
}

nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}

nav .title {
  color: white;
}
```

That's a lot of code, and it's readability is not exactly clean and easy. What if we were able to style elements almost the way we write them in HTML?

#### Never fear, Sass is here!

We can do just that with Sass. Let's rewrite that code from above using Sass nesting and see if we can clean it up, make it more readable, and more efficient to boot.

```css
nav {
  ul {
    margin: 0 auto;
    padding: 0;
    list-style: none;
  }

  li {
    display: inline-block;
  }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }

  .title {
    color: white;
  }
}
```

Wow! That is much more concise and the chance of us losing pieces of our nav styling while we are tinkering around with other styles is less likely. We simply created a `nav` element and inside of it we targeted our other elements as normally would outside, but without having to reference the `nav` element again. So you can see we placed a `ul`, `li`, `a`, and `.title` inside of our `nav` element.


**It should be noted that nesting to deeply, more than one or two elements as a rule of thumb, makes it difficult for CSS to be compiled correctly. Limit nesting to one or two elements deep**

### Conclusion
* Nesting elements with Sass is an effective way to not only organize your code, but to also be more efficient in the writing of it.
* Nesting simply requires that you nest children elements within their parent element, such as the navigation example.

#### References
* [Sass](http://sass-lang.com/guide)
