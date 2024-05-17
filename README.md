# SASS
Sass, or "Syntactically Awesome StyleSheets", is a language extension of CSS. It adds features that aren't available in basic CSS, which make it easier for you to simplify and maintain the style sheets for your projects.

In this Sass course, you'll learn how to store data in variables, nest CSS, create reusable styles with mixins, add logic and loops to your styles, and more.

Store Data with Sass Variables
    One feature of Sass that's different than CSS is it uses variables. They are declared and set to store data, similar to JavaScript.

    In JavaScript, variables are defined using the let and const keywords. In Sass, variables start with a $ followed by the variable name.

    Here are a couple examples:

    $main-fonts: Arial, sans-serif;
    $headings-color: green;
    And to use the variables:

    h1 {
    font-family: $main-fonts;
    color: $headings-color;
    }
    One example where variables are useful is when a number of elements need to be the same color. If that color is changed, the only place to edit the code is the variable value.

<style type='text/scss'>
    $text-color: red;

    .header{
      text-align: center;
    }
    .blog-post, h2 {
      color: $text-color;
    }
  </style>
  
  <h1 class="header">Learn Sass</h1>
  <div class="blog-post">
    <h2>Some random title</h2>
    <p>This is a paragraph with some random text in it</p>
  </div>
  <div class="blog-post">
    <h2>Header #2</h2>
    <p>Here is some more random text.</p>
  </div>
  <div class="blog-post">
    <h2>Here is another header</h2>
    <p>Even more random text within a paragraph</p>
  </div>

Sass allows nesting of CSS rules, which is a useful way of organizing a style sheet.

Normally, each element is targeted on a different line to style it, like so:

article {
  height: 200px;
}

article p {
  color: white;
}

article ul {
  color: blue;
}
For a large project, the CSS file will have many lines and rules. This is where nesting can help organize your code by placing child style rules within the respective parent elements:

article {
  height: 200px;

  p {
    color: white;
  }

  ul {
    color: blue;
  }
}
for example:
<style type='text/scss'>
  .blog-post {

 
  h1 {
    text-align: center;
    color: blue;
  }
  p {
    font-size: 20px;
  }
  }
</style>

<div class="blog-post">
  <h1>Blog Title</h1>
  <p>This is a paragraph</p>
</div>


In Sass, a mixin is a group of CSS declarations that can be reused throughout the style sheet.

Newer CSS features take time before they are fully adopted and ready to use in all browsers. As features are added to browsers, CSS rules using them may need vendor prefixes. Consider box-shadow:

div {
  -webkit-box-shadow: 0px 0px 4px #fff;
  -moz-box-shadow: 0px 0px 4px #fff;
  -ms-box-shadow: 0px 0px 4px #fff;
  box-shadow: 0px 0px 4px #fff;
}
It's a lot of typing to re-write this rule for all the elements that have a box-shadow, or to change each value to test different effects. Mixins are like functions for CSS. Here is how to write one:

@mixin box-shadow($x, $y, $blur, $c){ 
  -webkit-box-shadow: $x $y $blur $c;
  -moz-box-shadow: $x $y $blur $c;
  -ms-box-shadow: $x $y $blur $c;
  box-shadow: $x $y $blur $c;
}
The definition starts with @mixin followed by a custom name. The parameters (the $x, $y, $blur, and $c in the example above) are optional. Now any time a box-shadow rule is needed, only a single line calling the mixin replaces having to type all the vendor prefixes. A mixin is called with the @include directive:

div {
  @include box-shadow(0px, 0px, 4px, #fff);
}
 Mixins allow you to define reusable blocks of styles that can be included wherever needed, reducing duplication in your code.
 example:
 @mixin border-radius($radius) {
  -webkit-border-radius: $radius;
  -moz-border-radius: $radius;
  border-radius: $radius;
}

.button {
  @include border-radius(5px);
}

<style type='text/scss'>
  @mixin border-radius($radius){
    -webkit-border-radius: $radius;
  -moz-border-radius: $radius;
  -ms-border-radius: $radius;
 border-radius: $radius;
  }


  #awesome {
    width: 150px;
    height: 150px;
    background-color: green;

  }
  div {
    @include border-radius(15px);
  }
</style>

<div id="awesome"></div>

The @if directive in Sass is useful to test for a specific case - it works just like the if statement in JavaScript.

@mixin make-bold($bool) {
  @if $bool == true {
    font-weight: bold;
  }
}
And just like in JavaScript, the @else if and @else directives test for more conditions:

@mixin text-effect($val) {
  @if $val == danger {
    color: red;
  }
  @else if $val == alert {
    color: yellow;
  }
  @else if $val == success {
    color: green;
  }
  @else {
    color: black;
  }
}
Create a mixin called border-stroke that takes a parameter $val. The mixin should check for the following conditions using @if, @else if, and @else directives:

light - 1px solid black
medium - 3px solid black
heavy - 6px solid black
If the $val parameter value is not light, medium, or heavy, then the border property should be set to none.

<style type='text/scss'>
  @mixin border-stroke($val) {
    @if $val == light {
      border: 1px solid black;
    }
    @else if $val == medium {
      border: 3px solid black;
    }
    @else if $val == heavy {
      border: 6px solid black;
    }
    @else {
      border: none;
    }
  }


  #box {
    width: 150px;
    height: 150px;
    background-color: red;
    @include border-stroke(medium);
  }
</style>

<div id="box"></div>

The @for directive adds styles in a loop, very similar to a for loop in JavaScript.

@for is used in two ways: "start through end" or "start to end". The main difference is that the "start to end" excludes the end number as part of the count, and "start through end" includes the end number as part of the count.

Here's a start through end example:

@for $i from 1 through 12 {
  .col-#{$i} { width: 100%/12 * $i; }
}
The #{$i} part is the syntax to combine a variable (i) with text to make a string. When the Sass file is converted to CSS, it looks like this:

.col-1 {
  width: 8.33333%;
}

.col-2 {
  width: 16.66667%;
}

...

.col-12 {
  width: 100%;
}
This is a powerful way to create a grid layout. Now you have twelve options for column widths available as CSS classes.
<style type='text/scss'>
@for $j from 1 to 6 {
  .text-#{$j} {
    font-size: 15px * $j
  }
}


</style>

<p class="text-1">Hello</p>
<p class="text-2">Hello</p>
<p class="text-3">Hello</p>
<p class="text-4">Hello</p>
<p class="text-5">Hello</p>

Sass also offers the @each directive which loops over each item in a list or map. On each iteration, the variable gets assigned to the current value from the list or map.

@each $color in blue, red, green {
  .#{$color}-text {color: $color;}
}
A map has slightly different syntax. Here's an example:

$colors: (color1: blue, color2: red, color3: green);

@each $key, $color in $colors {
  .#{$color}-text {color: $color;}
}
Note that the $key variable is needed to reference the keys in the map. Otherwise, the compiled CSS would have color1, color2... in it. Both of the above code examples are converted into the following CSS:

.blue-text {
  color: blue;
}

.red-text {
  color: red;
}

.green-text {
  color: green;
}
Write an @each directive that goes through a list: blue, black, red and assigns each variable to a .color-bg class, where the color part changes for each item to the respective color. Each class should set the background-color to the respective color as well.

<style type='text/scss'>
$colors: blue, black, red;

@each $color in $colors {
  .#{$color}-bg {
    background-color: $color;
  }
}

  div {
    height: 200px;
    width: 200px;
  }
</style>

<div class="blue-bg"></div>
<div class="black-bg"></div>
<div class="red-bg"></div>


The @while directive is an option with similar functionality to the JavaScript while loop. It creates CSS rules until a condition is met.

The @for challenge gave an example to create a simple grid system. This can also work with @while.

$x: 1;
@while $x < 13 {
  .col-#{$x} { width: 100%/12 * $x;}
  $x: $x + 1;
}
First, define a variable $x and set it to 1. Next, use the @while directive to create the grid system while $x is less than 13. After setting the CSS rule for width, $x is incremented by 1 to avoid an infinite loop.

<style type='text/scss'>

$x: 1;
@while $x < 6 {
  .text-#{$x} {
    font-size: 15px * $x;
    $x: $x + 1;
  }
}

</style>

<p class="text-1">Hello</p>
<p class="text-2">Hello</p>
<p class="text-3">Hello</p>
<p class="text-4">Hello</p>
<p class="text-5">Hello</p>


Partials in Sass are separate files that hold segments of CSS code. These are imported and used in other Sass files. This is a great way to group similar code into a module to keep it organized.

Names for partials start with the underscore (_) character, which tells Sass it is a small segment of CSS and not to convert it into a CSS file. Also, Sass files end with the .scss file extension. To bring the code in the partial into another Sass file, use the @import directive.

For example, if all your mixins are saved in a partial named "_mixins.scss", and they are needed in the "main.scss" file, this is how to use them in the main file:

@import 'mixins'
Note that the underscore and file extension are not needed in the import statement - Sass understands it is a partial. Once a partial is imported into a file, all variables, mixins, and other code are available to use.
Write an @import statement to import a partial named _variables.scss into the main.scss file.

To import a partial named _variables.scss into your main.scss file, you can use the @import directive. Here's how you would do it:

Ensure your _variables.scss file is named correctly and is in the same directory as your main.scss file, or adjust the path accordingly if it is in a different directory.
Use the @import directive in main.scss to import _variables.scss.
Here’s the @import statement:

scss
Copy code
@import 'variables';
Here's an example of what your main.scss file might look like:

scss
Copy code
@import 'variables';

// Other SCSS code
In this example:

The underscore (_) and the file extension (.scss) are omitted in the @import statement. This is a SCSS convention for importing partials.
Make sure the path is correct. If _variables.scss is in a different directory, you would need to specify the path relative to main.scss.
For example, if _variables.scss is in a folder named partials, you would write:

scss
Copy code
@import 'partials/variables';



Sass has a feature called extend that makes it easy to borrow the CSS rules from one element and build upon them in another.

For example, the below block of CSS rules style a .panel class. It has a background-color, height and border.

.panel{
  background-color: red;
  height: 70px;
  border: 2px solid green;
}
Now you want another panel called .big-panel. It has the same base properties as .panel, but also needs a width and font-size. It's possible to copy and paste the initial CSS rules from .panel, but the code becomes repetitive as you add more types of panels. The extend directive is a simple way to reuse the rules written for one element, then add more for another:

.big-panel{
  @extend .panel;
  width: 150px;
  font-size: 2em;
}
The .big-panel will have the same properties as .panel in addition to the new styles.

.info-important{
   @extend .info;
   background-color: magenta;
 }



</style>
<h3>Posts</h3>
<div class="info-important">
  <p>This is an important post. It should extend the class ".info" and have its own CSS styles.</p>
</div>

<div class="info">
  <p>This is a simple post. It has basic styling and can be extended for other uses.</p>
</div>


