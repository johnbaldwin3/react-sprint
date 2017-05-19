## Regular Expressions
> "Some people, when confronted with a problem, think 'I know, I’ll use regular expressions.’
> Now they have two problems."
>
> *Jamie Zawinski*

Well that may be partially true, but that's not giving credit to just how powerful regular expressions can be. Regular expressions, sometimes referred to in short as "RegEx", are type of object that is entirely suited for the job of sorting, processing, and inspecting strings.

### What is it and how does it work?

By now we should be getting very comfy and cozy with JavaScript objects. You should be starting to see just how versatile they are in all of the different applications we have looked at. Regular expressions are no different. Let's first take look at how they can be created.

#### RegExp : The constructor function.

The first way that we can create a regular expression is to use the `RegExp` constructor. Don't be concerned with how the function works just yet, let's just take in the basics of how to make one.

```js
var regularExpression = new RegExp("xyz");
```

That's it! We create a new instance using the `new` keyword and the `RegExp` constructor - `regularExpression` is now actually a regular expression!

#### Object literal: Just the bare facts.

We can also create regular expressions by using a special JavaScript language dedicated solely to regular expressions. This is going to seem very confusing at first but we will dive deeper after we first learn to swim in these crazy RegEx waters. Let's recreate the same regular expression from above in a different format.

```js
var regularExp = /xyz/ ;
```

This code and the previous code do the same thing! Notice the `/` that contain the `xyz` in the literal format, whereas in the `regularExpression` created by the the `new RegExp` we simply used `"xyz"`. One of the fundamental differences is that the `RegExp` takes in a string as its argument. The literal method takes in a kind of different syntax using backlashes.

### So that's cool, I think, but what does it do?!

Let's start simple. We learned that regular expressions deal with strings (sorting, matching, testing, etc.). Let's create a very simple test using the baked in `test` function that comes with each regular expression. `test` will return a boolean `true` or `false` if the criteria are met or not.

Let's say we wanted to find out if a string contained the word dog anywhere in it, inside of words, as a stand alone word, etc. More simple, we are going to search to see if the letters 'd', 'o', and 'g', appear consecutively anywhere within a string passed into our regular expression. It must match exactly those characters.

```js
var dogReg = /dog/;

console.log(dogReg.test("dog"));
console.log(dogReg.test("a dog is cool"));
console.log(dogReg.test("doggy"));
console.log(dogReg.test("snoop dog"));
console.log(dogReg.test("abcdedogfghij"));
//all outputs => true;


//Now, let's see what fails.. and returns false...
console.log(dogReg.test("Dog"));
console.log(dogReg.test("a d o g is cool"));
console.log(dogReg.test("Snoop Dog"));
console.log(dogReg.test("abcded ogfghij"));
//all outputs => false;

```

As you can see, our regular expression must match exactly, including case, given the parameters we passed into it. There can be no spaces either. It needs to find 'dog' all together to return true.

We can introduce another special character that would help us determine if a capitol or lowercase 'd' was used in dog. Let's take a look at the `|` character in the expression.

```js
var tigerReg = /t|Tiger/;

console.log(tigerReg.test("Tiger"));
console.log(tigerReg.test("tiger"));
console.log(tigerReg.test("abcdeTigerfghijk"));
// all outputs => true;
```

By using setting the expression to `/t|Tiger/` we check to see if the 't' or the 'T' character are used to begin the word tiger, if either is present and all the characters are consecutive, this test will pass.

We can take that one stripe of a tiger further and apply the `i` to the end of the expression which will make the expression "case insensitive", meaning it doesn't care if it is all capitols or doesn't include capitol letters.

We could rewrite the above code as follows:

```js
var tigerReg = /tiger/i;
```

This will still pass all of the tests above, but don't forget the `|` operator, as it can come in handy still down the road when testing if one word or another is contained, etc.

Similar to the `|` operator the `?` will search for a string that may or may not contain a certain character or word. Let's take a look to better explain. Let's say we were searching through an article that was randomly using British spelling for words such as "colour", but it wasn't consistent so we needed to check for the word "color" too... Using the `?` allows us to include a character or word but doesn't make it a requirement.

```js
var colorReg = /colou?r/;

console.log(colorReg.test("I like colors"));
console.log(colorReg.test("That colour was rubbish!"));
//all outputs => true;
```

So, these are some of the basics, but let's see how this would function in the real world. Let's author a test to see if some text input is in the format we were expecting. We will throw in some of the other goodies and then explain them after the example.

```js
function theRingerCheck(phoneNumber) {
  var phoneNumberReg = /^\(\d\d\d\)\s?\d\d\d\s?-\s?\d\d\d\d$/;

  if (phoneNumberReg.test(phoneNumber)){
    console.log("The phone number is good to go");
  } else {
    console.log("You aren't fooling anyone with that fake number");
  }

}

var thePhoneNumber = "(864)555-5555";
var thePhoneNumber2 = "(864) 555 - 5555"
var theFakeNumber = "(86)5210123";

theRingerCheck(thePhoneNumber);
//output => "The phone number is good to go"

theRingerCheck(thePhoneNumber2);
//output => "The phone number is good to go"

theRingerCheck(theFakeNumber);
//output => "You aren't fooling anyone with that fake number"
```

Wow, that looks confusing, but let's break it down and behold the power of the regular expression.
We created a function `theRingerCheck` that took in a phone number. Inside of the function we created a regular expression with the variable name `phoneNumberReg`. In that regular expression we threw in a few new operators, so let's take a quick peek at those:

* The `^` operator simply let's the search no that it must begin with the following search criteria (as opposed to matching anywhere in a string).

* Next you can see we used `\(` which just let's the search know we are not using the `()` operators and instead we are looking for the `(` character in our string. Using the `\` will let the search know you are looking for that character not using it as a search operator. We also do the same at the end of the first set with the closing parenthesis.

* Following that you see the `\d` which is a special operator that searches for any digit [0-9], so our first portion of the regular expression is really saying that we are looking for **(###)**. i.e (864).

* Next we use the `\s` operator coupled with our friend `?`. This just says that it is okay if there is a white-space in between the (123) and the following digits 555. `\s` is for the white-space, and the `?` let's the search know it is valid with or without it.

* We then add three more digits and another optional space. We follow that up with a `-` which means that we want to make sure that a dash is included. Another optional space and then four more digits. All pretty straight forward.

* The last operator, `$`, let's the search know that it should be the end of the string, meaning nothing else should be tacked on past it.

* Let's now look at what this really says in plain english to make sure we understand: "We want to validate a string that begins with a ( and ends with a numerical digit. In between that we want to make sure we have 3 digits followed by a ). We can have a space in between or not, then 3 more digits, followed by an optional space. We then want to make sure there is a dash, which can be followed by an optional space, and then 4 more digits with nothing else following that".

That's a lot to take in and that's really just the tip of the iceberg. Regular expressions are extremely powerful and use a complicated syntax that takes a lot of practice to master.

### Conclusion

* Regular expressions are a built in JavaScript object `RegExp`.
* Regular expressions can be declared with the `new` constructor or expressed as a literal.
* Regular expressions are a means for sorting and searching strings in JavaScript for patterns.
* *Please* take a look at the reference material, there is a ton to learn if you are interested in regular expressions! ! !

#### References
* [MDN Regular Expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)

* [Eloquent JavaScript - Regular Expressions](http://eloquentjavascript.net/09_regexp.html)
