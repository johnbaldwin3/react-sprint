## Leveling Up with Sass

Sass is a style language designed to enhance CSS. Sass or "Syntactically Awesome Style Sheets" is a tool that allows you to create variables, mixins, partials, and imports - all of which we will touch on in later lessons. Sass uses a preprocessor (run in terminal) that compiles your **.scss** or "Sassy CSS" file into a regular **.css** file that the browser recognizes.  

### Why Sass?

Styling web applications can be a huge job, especially on extensive projects. The ability to use repeatable code, like variables, would be a huge help in efficiency and maintainability. Let's picture for instance a web application that has 30-40 uses of a single color spread out through hundreds of lines of code. You take your final product to the graphic design team, and they suggest changing that color to one shade darker. Congratulations, you've got some more work on your hands to get that all fixed.

Same scenario, but let's say that you have stored all of your colors in variables, and you can simply go to one spot at the top of your stylesheet and change the color value for that variable the graphic design team wanted changed, and the rest of your project is fixed, just like that!

Well in standard CSS that's just not an option yet, but let's welcome our special guest Sass to the stage.

### Installing Sass [http://sass-lang.com/install](http://sass-lang.com/install).

You should already have Ruby installed on your computer and in terminal you should run the command:

```
sudo gem install sass
```

This globally installs Sass on your machine and this command *will not need to be run again*.

### Once installed

After you have created a project directory, you're going to need to turn on the preprocessor so we can compile our ".scss" into a ".css" file. To do that, we need to make sure we are inside of our project directory in terminal.

In the project folder run the following command in terminal:

```
sass --watch scss:css
```

This turns on a watch that looks over your directory for any '.scss' files and listens for changes to those files. When a change occurs the preprocessor compiles that change and stores it in your main '.css' folder.

**This command runs indefinitely and will continue to run until you kill it with " Control + C "**

Now any styling should be done inside of the ".scss" document, which will be rendered using the compiled CSS.


### Conclusion
* Sass is a preprocessor for CSS that allows for more efficient styling.
* Sass uses a file with the extension '.scss' (or Sassy CSS).
* Sassy CSS files are compiled into CSS that the browsers can read.
* Sass needs to only be installed once globally.
* Inside of a project directory, running the `sass --watch scss:css` command turns on a watch that listens for changes from a '.scss' file and compiles them into a '.css' file.
* Using "Control" and "C" at the same time (Control + C) will kill the Sass watch compiler.

#### References

* [Sass](http://sass-lang.com/guide)
