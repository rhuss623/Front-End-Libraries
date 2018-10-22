# Sass Notes
Hi! My name is Ryan Hussey and these are my personal notes for freeCodeCamp's jQuery lessons.<br>Feel free to use them if they are useful to you.

Nest Sass in:
```HTML
<style class="sass">

</style>
```
### Store Data with Sass Variables

To declare variables, use <span style=color:red>$</span> followed by the variable name.
```JavaScript
$text-color: blue;
```
To use the variable:
```CSS
h1, p {
  color: $text-color;
}
```
### Nest CSS with Sass

Nesting can be used to organize children and parent elements in CSS w/ Sass.  In the example below .blog-post is the parent of h1 and p.

```CSS
.blog-post {
    background-color: gray;
  h1 {
    text-align: center;
    color: blue;
  }
  p {
    font-size: 20px;

    }
  }
```
### Create Reusable CSS with Mixins
A <span style=color:red>mixin</span> is a group of CSS declarations that can be reused.

To define a <span style=color:red>mixin</span>, use <span style=color:red>@mixin</span> followed by the name of the <span style=color:red>mixin</span> and optional parameters w/in parentheses.
e.g.
```JavaScript
@mixin sample($a, $b, $c){
  ...
}
```
In freeCodeCamp's example, they use:
```JavaScript
@mixin box-shadow($x, $y, $blur, $c){
  -webkit-box-shadow: $x, $y, $blur, $c;
  -moz-box-shadow: $x, $y, $blur, $c;
  -ms-box-shadow: $x, $y, $blur, $c;
  box-shadow: $x, $y, $blur, $c;
}
```
as a mixin replacement for:
```JavaScript
div {
  -webkit-box-shadow: 0px 0px 4px #fff;
  -moz-box-shadow: 0px 0px 4px #fff;
  -ms-box-shadow: 0px 0px 4px #fff;
  box-shadow: 0px 0px 4px #fff;
}
```
To call the <span style=color:red>mixin</span>, use <span style=color:red>@include</span>
To call the <span style=color:red>mixin</span> above, freeCodeCamp used:
```JavaScript
div {
  @include box-shadow(0px, 0px, 4px, #fff);
}
```
### Use @if and @else to Add Logic To Your Styles

One can use <span style=color:red>@if</span>, <span style=color:red>@else if</span>, and <span style=color:red>@else</span> sass statements just as one would use if, else if, and else statements in JavaScript.

Here's an example from freeCodeCamp:

```JavaScript
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
```

### Use @for to Create a Sass Loop
<span style=color:red>@for</span> directives loop through elements.  A "start <span style=color:blue>through</span> end" <span style=color:red>@for</span> loop includes the end number and a "start <span style=color:blue>to</span> end" <span style=color:red>@for</span loop excludes the end number.

freeCodeCamp's example creates a twelve equally spaced columns w/ a <span style=color:red>@for</span> directive:
```JavaScript
@for $i from 1 through 12 {
  .col-#{$i} { width: 100%/12 * $i; }
}
```
The ${} is used to make the variable into a string.
Here's another example:
```HTML
<style type='text/sass'>
 @for $j from 1 to 6 {
 .text-#{$j} {
 font-size: $j * 10px;
 }
 }


</style>

<p class="text-1">Hello</p>
<p class="text-2">Hello</p>
<p class="text-3">Hello</p>
<p class="text-4">Hello</p>
<p class="text-5">Hello</p>
```
### Use @each to Map Over Items in a List
<span style=color:red>@each</span> will iterate through a list or map.  If we wanted to assign a color to text based on a name (as in the freeCodeCamp example we'll see below) we can use <span style=color:red>@each</span> to do so.

Here's our goal:
```CSS
.blue-text {
  color: blue;
}

.red-text {
  color: red;
}

.green-text {
  color: green;
}
```
If a list is used, the syntax would be:
```CSS
@each $color in blue, red, green {
  .#{$color}-text {color: $color;}
}
```
and if using a map:
```CSS
$colors: (color1: blue, color2: red, color3: green);

@each $key, $color in $colors {
  .#{$color}-text {color: $color;}
}
```
### Apply a Style Until a Condition is Met with @while
<span style=color:red>@while</span> works like a <span style=color:red>while</span> loop in JavaScript.  
The example below sets a variable <span style=color:red>$x</span> to 1 and increments the variable. The function in the loop will continue until <span style=color:red>$x</span> is 10.
```HTML
<style type='text/sass'>
  $x: 1;
  @while $x < 11 {
  .text-#{$x} {
  font-size: $x * 5px;
    }
  $x: $x + 1;
  }


</style>

<p class="text-1">Hello</p>
<p class="text-2">Hello</p>
<p class="text-3">Hello</p>
<p class="text-4">Hello</p>
<p class="text-5">Hello</p>
<p class="text-6">Hello</p>
<p class="text-7">Hello</p>
<p class="text-8">Hello</p>
<p class="text-9">Hello</p>
<p class="text-10">Hello</p>
```
### Split Your Styles into Smaller Chunks with Partials

A partial is a file holding segments of CSS code.  These can be imported using <span style= color:red>@import</span> and the convention for naming the files is to begin w/ an underscore and end the filename w/<span style=color:red> .scss</span>.

To import a partial named "_variables.scss" use:
```JavaScript
@import 'variables'
```
### Extend One Set of CSS Styles to Another Element
Extending allows you to take the style of one element and apply it to another element, as is shown here:
```CSS
.info{
    width: 200px;
    border: 1px solid black;
    margin: 0 auto;
  }
  .info-important{
  @extend .info;
  background-color: magenta;
  }
```
