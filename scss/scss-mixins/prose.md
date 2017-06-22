## Using Sass Mixins and Extending Inheritance

Another amazing thing that Sass can do for us revolves around the world of mixins. The simplest means of thinking about mixins is to treat them much like a variable in Sass. The power of mixins is that they can hold chunks of code as a variable and even allow for arguments to be passed in as values.

We can also extend one element's properties to another in a very easy fashion, even furthering our ability to be efficient and DRY in our coding.


### There's no mixup with the power of mixins!

Let's pretend for a moment that we are authoring an amazing blog website. Each blog is going to be styled the same, but each blog may differ in some aspect, so we can't just blanket the blogs with a class and make them all the same. This would be a real pain if most of the styling was the same and we had to repeat it over and over again.

True, we could save some time with our Sass variables, good thinking! But what if we could save even more time? You guessed it, we can! Using Sass mixins opens to door to even more efficiency in our styling. Don't believe me? Let's check it out!

To illustrate this as simply as possible we will leave out all other variables and goodies for now, we can revisit those in a bit. Let's create a mixin for our blog called `blog-style` and then use that mixin in a few of our different imaginary blog classes. We will take note of the `@mixin` and `@include` statements to see their functionality.

```css
@mixin blog-style {
  font-size: 20px;
  font-family: Helvetica, sans-serif;
  color: #F66733;
  font-weight: bold;

}

.blog1 {
  @include blog-style;
  border: 1px solid purple;
}

.blog2 {
  @include blog-style;
  border: 1px solid orange;
}
```

That makes life easy, especially if you had 15-20 blogs to style, or more. We simply created a mixin `blog-style` by declaring our mixin with the `@mixin blog-style { }` statement. We then declared our styles inside of it. In order for us to use our new mixin we simply added the `@include blog-style;` statement in each element where we wanted to have those styles applied.

#### Mixins getting in arguments

Not only can mixins store multiple variables and easily let you replicate them with little code repetition, but mixins can actually take in arguments like a function in JavaScript. Let's take a look at the code above and refactor it using a mixin that is set to take arguments.

```css
@mixin blog-style ($border, $width) {
  font-size: 20px;
  font-family: Helvetica, sans-serif;
  color: #F66733;
  font-weight: bold;
  border: $border;
  width: $width;
}

```

Before we see how this is applicable in styling, let's note just a few quick points. After we declared our mixin `@mixin blog-style` we passed in parenthesis like so - `@mixin blog-style ($border, $width) { }`. Inside of the parenthesis we passed in two separate variables (but you can have more or less, **though think of 6-7 as a max to keep confusion down**). We then gave the properties `border` and `width` the values of those variables - `border: $border` and `width: $width`.

Hopefully that is pretty clear and easy to follow, now let's see how these would be applied to our blog. We want to create a different border and width for each blog, but all other styles should be the same.

```css
@mixin blog-style ($border, $width) {
  font-size: 20px;
  font-family: Helvetica, sans-serif;
  color: #F66733;
  font-weight: bold;
  border: $border;
  width: $width;
}

.blog1 {
  @include blog-style(1px solid purple, 200px);
}

.blog2 {
  @include blog-style(4px dashed orange, 400px);
}

```

Okay, so what did we do? We used our `@include` to give each blog access to our mixin, but then we also added our parenthesis and passed in the values for our variable arguments separated by commas for each argument.

We defined a border of `1px solid purple` in `.blog1` and then followed it with a comma and passed in a width property of `200px`. The mixin then applies those values to the variables, allowing us to adjust those values as necessary for each instance. How efficient is that?

#### Extending properties

Let's take a look at another awesome feature of Sass. The `@extend` statement allows us to take one elements styling and extend it to another to save time and effort!

Let's imagine you have been developing a special `<div>` to hold pop up information, or something along those lines. We will give that a class of `.popup`. Let's style our first popup below.

```css
.popup {
  border: 1px solid black;
  border-radius: 15px;
  text-shadow: 1px 1px 1px black;
  box-shadow: 1px 3px 2px black;
  font-size: 20px;
  font-family: Helvetica, sans-serif;
  color: orange;
  background-color: purple;
}

```

That's a lot of style to repeat if we were so inclined... and guess what, we are!
We've decided that we should create a few more popups with the same style, but maybe we will just change the color of the border for each one. Alright... get to it, hope your fingers are ready to type.

Just kidding, let's use the `@extend` property and save a bunch of time so we can go grab some food instead.

```css
/* Here's our first div */
.popup {
  border: 1px solid black;
  border-radius: 15px;
  text-shadow: 1px 1px 1px black;
  box-shadow: 1px 3px 2px black;
  font-size: 20px;
  font-family: Helvetica, sans-serif;
  color: orange;
  background-color: purple;
}

/*Let's style a few more below it */

.popup2 {
  @extend .popup;
  border-color: purple;
}

.popup3 {
  @extend .popup;
  border-color: orange;
}

```

So what did we do? Well using `@extend .popup;`, we extended the `.popup` class to our other two classes `.popup1` and `.popup2`. Any styles we give those other popups will override the original styling of `.popup`, which is why were able to change the color of the border from black to purple and orange. That's all there is to it! `@extend` give us a lot of power to write DRY code and save our fingers from typing a lot of extra nonsense! Sass, you are my best friend!

### Conclusion
* Mixins are customizable chunks of code that can be inserted into elements to save time and increase efficiency.
* Mixins can take in arguments as variables and allow for big chunks of code to also be customizable as needed.
* To create a mixin, simply use the `@mixin "your mixin name" { }` statement. You can pass variables to the mixin inside of parenthesis with the `$` such as `$border` and `$width` by separating them with commas, for example `@mixin blog-style ($border, $width) { }`.
* To use a mixin call it within the styling of an element with an `@include "your mixin name";` statement. i.e. `@include blog-style(1px solid purple, 200px);` Pass any arguments you might have set up on your mixin separated by commas as seen here.
* Using `@extend` allows one element to inherit another element's styles. Any other stylings given to the child element will take precedence.

#### References

* [Sass](http://sass-lang.com/guide)
