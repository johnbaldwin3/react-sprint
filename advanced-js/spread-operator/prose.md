## The Spread Operator

Yet another great gift of ES2015 come with the spread operator `...`. This harmless little ellipsis can actually great, mysterious, and magical things. We are going to examine the role that the spread operator can play when working with Arrays. We can use it to copy arrays, to concatenate arrays, and as a powerful array literal tool while concatenating one array into another part of an array.

The spread operator's job is to expand an array into it's elements... which provides a powerful aid in methods listed above.  

### Copying Arrays with the spread operator

Prior to `...`, copying arrays had to be completed using `Array.slice()` method. We've already examined quite a bit of that already, so let's take a look at the new means to copy - our friend the spread operator.

```js
var yearsMichaelJordanWon = [1991, 1992, 1993, 1996, 1997, 1998];
var greatYears = [...yearsMichaelJordanWon];

console.log(greatYears);
// output => [1991, 1992, 1993, 1996, 1997, 1998]
```

Here's what we did - we created an array `yearsMichaelJordanWon` and gave it some dates (that he won NBA Championships!). We wanted to copy that array into a new array, `greatYears`, so we set `greatYears` value equal to `...yearsMichaelJordanWon`. It's that simple. We logged out what `greatYears` had as an array and it is an exact copy of `yearsMichaelJordanWon`! Wow! That's a lot of trophies!

### Concatenation got your tongue?

Merging two arrays in to one, could sometimes be a great deal of work. With the use of the `...` operator, we can do this very simply and efficiently as follows:

```js

var arrayUno = ["Uno", "Dos", "Tres"];

var arrayDos = ["Cuatro", "Cinco", "Seis"];

var arrayUnoYDos = [...arrayUno, ...arrayDos];

console.log(arrayUnoYDos);
//output => ["Uno", "Dos", "Tres", "Cuatro", "Cinco", "Seis"]
```

Using the spread operator we simply created a new array `arrayUnoYDos` and declared its value as `[...arrayUno, ...arrayDos]`. This swiftly, efficiently, and magically combined our two arrays into what we see in the `console.log` statement `["Uno", "Dos", "Tres", "Cuatro", "Cinco", "Seis"]`. Muy facil! ("Easy").

### The power of an Array literal in concatenation

We can take this one step further and see how easy it is to place one array inside of a different array. Previously this would have taken a lot of fun things like `splice`, `push`, and `concat`. Now, we can just put the car in cruise control and coast with the spread operator!

```js
var goShawty = ["It's", "your", "birthday", "We", "gon'", "party"];
var yourBirthday = ["go", "shawty", ...goShawty, "like", "it's", "yo", "birthday", "We", "gon'", "sip", "Bacardi", "like", "it's", "your", "birthday"];

console.log(yourBirthday);
//output => ["go", "shawty", "It's", "your", "birthday", "We", "gon'", "party", "like", "it's", "yo", "birthday", "We", "gon'", "sip", "Bacardi", "like", "it's", "your", "birthday"]
```

So by adding the `...goShawty` array into our `yourBirthday` array, we get the complete output for the first lines of "In 'da Club'"! Now that's what I am talking about!



#### Only for iterables!

  It's important to note that the spread operator only works on iterables - meaning only on data that can be mapped over (like an array!). In complex arrays that have arrays and objects nested inside of them, the spread operator may not be the best choice to extract data.

### Conclusion
* The spread operator can expand an array it it's singular elements.
* The spread operator can be used to make copies of an array.
* The spread operator can be used to concatenate arrays together.
* The spread operator can be used to merge arrays together at any index as an Array literal.
* The spread operator should not be used to iterate over complex arrays with deep seeded values.

#### References

- [MDN Spread Operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)
