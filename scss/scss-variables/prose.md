## Sass Variables

When we first introduced Sass, we laid a scenario out where you, the software engineer, met with a design team. The design team decided that first shade of color they didn't like and wish they had gone one shade darker. They ask you ever so politely to go back and change all of the instances where you used that color and make them the new color.

Whew! That was a lot of work. You just get finished with that and they determine that not only do they like that color, but the complimenting color they had originally decided needs to be changed to match the new one, so they ask you to go and replace that as well.

You start to step out of their office and they stop you to mention that maybe the font for all of the articles needs to be changed to a new font and the font size in each of the subsections of the articles should be a bit larger.

Looks like you've got a lot of work left, and you still have some serious JavaScript to write for the functionality of the program! Why Design Team, Why????????

Well don't fear, you installed Sass remember. This is going to be a breeze and you'll be back to programming functionality in no time.

### Creating Variables

As in JavaScript, Sass variables provide the same ability to store information to be used over and over again. Writing Sass variables is easy work so let's take a look at how the implementation from our story above might look (on a very scaled down version). We are going to declare a variable for two separate colors, a font-stack, and for a font-size.

Just like in JavaScript, variables can be named whatever you would like, but keeping the names tied with meaning will help you organize them. All variables in Sass begin with a `$`.

```css
/*Variables*/

$mainColor: #F66733;
$secondaryColor: purple;
$fontStack: Helvetica, sans-serif;
$mainFontSize: 40px;
$secondaryFontSize: 20px;


/*Styling*/

.headline {
  color: $mainColor;
  font-size: $mainFontSize;
  font-family: $fontStack;
}

.paragraph1 {
  color: $secondaryColor;
  font-size: $secondaryFontSize;
}

```

So let's take a closer look at what we did. First at the top of our stylesheet we declared our variables. We used the `$` and named them as semantically as possible so that they are easily understood to us and others that might read our code. We declared 5 variable total. `$mainColor`, `$secondaryColor`, `$fontStack`, `$mainFontSize`, and `$secondaryFontSize`. After each variable we use a semi-colon to separate the variable name from the value we intend to give it. Values can be given for any valid value you would give a CSS element. So you can see above we declared a color `#F66733` as a hexadecimal number and we also declared a color `purple` as a simple text color.
We listed a font family and we also aside a font size. All valid, all helpful.

To assign those variables as we would assign an element properties in CSS, we simply select our element, for instance the class `.headline` (that would correspond to a class used in our HTML) and give it a property and value, such as `color: $mainColor;`. The only difference is that instead of giving it a direct value you pass it the variable you declared up at the top of the stylesheet!!! Holy cow that is cool!

#### How does it help?

Well, to make our changes, we simply go to one spot and change all the instances where those variables were used to whatever new value we want to try. Presto, job complete with 5 lines of code, instead of find and replacing possibly hundreds.

Hopefully the wheels are spinning and you are beginning to think of great things and increased efficiency! Well, like a TV infomercial stay tuned, there's more in the coming lessons!

### Conclusion
* Variables are nice and neat way to keep track of and change your CSS properties and values.
* Using variables is very simple. Declare them using a `$` at the top of your stylesheet.
* Put the variables into play by using them the way you would normally style elements : `body {color: $myColor;}`.

#### References

* [Sass Guide](http://sass-lang.com/guide)
