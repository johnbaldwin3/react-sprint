## Map, Reduce and Filter functions

At this point in your coding career, the `forEach` loop is probably your best bud. And while `forEach` is a great and useful function, you're about to meet some new pals who will show you a whole new way of programming. Sorry `forEach`, it's time for us to move on. Now let's learn about functional programming.

So far, you've probably been building and manipulating arrays of numbers, strings, and objects. In the past, the `for` loop was what we used to iterate over the elements in an array. But now we have the powerful tools `map`, `reduce`, and `filter` to help us split, search, sort, crunch numbers, and more. These three methods allow us to manage arrays efficiently and elegantly. See elegant image below:

![Map-Filter-Reduce](map-filter-reduce-in-emoji-1.png)

### Map

The `map` function allows you to perform an operation on all elements in an array and return a new array of the same length with the transformed contents. Let's look at a simple example to demonstrate:

```js
// Below is the way we would handle doubling numbers in an array with a for loop
var numbers = [1, 2, 3, 4];
var doubledNumbers = [];

for(var i = 0; i < numbers.length; i++){
  doubledNumbers[i] = numbers[i] * 2;
};

console.log("The doubled numbers are", doubledNumbers); // logs The doubled numbers are 2, 4, 6, 8
```

The above code works, but it's a little cumbersome to perform such a simple task. Now let's try it using the map function:

```js
var numbers = [1, 2, 3, 4];

var doubledNumbers = numbers.map(function(number){
  return number * 2;
});

console.log("The doubled numbers are", doubledNumbers); // logs The doubled numbers are 2, 4, 6, 8
```

Ah, such nice clean code. With the map function, you no longer need a loop, nor do you need to worry about indexing the array or creating a new array. Map does it for you. The `map` function traverses the array from left to right, invoking the callback function on each element in the array, and then returns a new array with the new values for each element.

An important thing to note: Never modify the 'state' in a map function. A callback should only modify the new value that's being returned from *that* callback.


### Filter
Ok, but maybe you only want to double the odd numbers in the array. The even numbers are not needed. In this scenario, `map` needs to call in it's buddy `filter`. Filter is great for when you want to remove unwanted elements from an array. Without `filter`, you'd have to write your code like this:

```js
var numbers = [1, 2, 3, 4];
var doubledNumbers = [];

for(var i = 0; i < numbers.length; i++) {
  if numbers[i] % 2 !== 0) {
    doubledNumbers[i] = numbers[i] * 2;
  }
}

console.log("The doubled numbers are", doubledNumbers); // logs The doubled numbers are 2, 6
```

Instead, we can use `map` and `filter` functions to simplify the process:

```js

var numbers = [1, 2, 3, 4];

var doubledNumbers = numbers.filter(function(number){
  return (number % 2 !== 0);
}).map(function(number){
  return number * 2;
});

console.log("The doubled numbers are", doubledNumbers); // logs The doubled numbers are 2, 6

```

In the above example, you can see that we were able to chain the map function onto the previous filter function. The return value of the filter function must be a boolean targeting which elements will be kept or discarded. The function then returns only elements of the array that meet the requirements of the boolean.

### Reduce

So what if you want to get the sum of the doubled numbers? The `reduce` method allows you to combine elements of an array and reduce them into a single value.

```js
//first, here's the slightly longer way to do it. Use map to double the numbers. Create a function that adds the numbers. Then invoke the reduce function on the doubled numbers array, passing it the add function.

var numbers = [1, 2,  3, 4];

var doubledNumbers = numbers.map(function(number){
  return number * 2;
});
var add = function(total, number){
  return total + number;
};
var totalNumber = doubledNumbers.reduce(add, 0);

console.log("The total number is", totalNumber); //logs The total number is 20
```

Notice that the second argument in the reduce function is set to zero - this establishes that we want the totalNumber variable to be a number. Now let's do that again in a more condensed way:

```js
var numbers = [1, 2,  3, 4];

var totalNumber = numbers.map(function(number){
  return number * 2;
}).reduce(function(total, number){
  return total + number;
}, 0);

console.log("The total number is", totalNumber); //logs The total number is 20
```

Here, we chained the reduce function and passed an un-named function straight in as the first parameter.

Similar to `map` and `filter`, `reduce` traverses an array from left to right. It invokes a passed in callback function on each element, then returns the cumulative value. *The reduce callback always expects the new total value to be returned.*

#### Chaining

In both the reduce and filter examples above, you saw examples of chaining functions. Chaining functions together is a nice way to consolidate your code. And with the map and filter functions, they both return arrays, so technically you could continue chaining them indefinitely.


### Conclusion

- Map: Use when you want to perform a function/transform each element in an array. Returns a new array of the same length.
- Filter: Use when you want to remove elements from an array based on a specific condition. Returns an array.
- Reduce: Use when you want to combine the elements of an array into a cumulative or concatenated value. Returns a single value.

Now go play with your new friends.

#### References

[Site point](https://www.sitepoint.com/map-reduce-functional-javascript/)

[Dan Martensen](https://danmartensen.svbtle.com/javascripts-map-reduce-and-filter)
