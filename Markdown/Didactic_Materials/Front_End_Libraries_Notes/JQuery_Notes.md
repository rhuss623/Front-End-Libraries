# jQuery Notes
Hi! My name is Ryan Hussey and these are my personal notes for freeCodeCamp's jQuery lessons.<br>Feel free to use them if they are useful to you.

First, any JavaScript, including jQuery, will run in an HTML file if it's w/in a script tag.
```HTML
<script></script>
```
To make the code run as soon as the browser page opens, use:
```HTML
<script>
$(document).ready(function() {
});
</script>
```

### Target HTML Elements with Selectors Using jQuery

Use a <span style=color:red>$</span> selector to start a jQuery function for jQuery.

To select an HTML element, use the following format:
```JavaScript
$("button").addClass("animated bounce");
```
The example above has selected all HTML buttons and added a class that makes them all bounce.
To select element by id, use <span style=color:red>#</span>, or by class w/ <span style=color:red>.</span>  e.g.
```JavaScript
$("#elementID").addClass("animated fadeOut")
$(".elementClass").addClass("shake")
```
### Change the CSS of an Element Using jQuery
Use <span style = color:red>.css()</span> function, e.g.
```JavaScript
$("#target1").css("color", "blue");
```

### Disable Elements using jQuery
The <span style = color:red>.prop()</span> function will change properties of an element. The example below disables the button element(s).
```JavaScript
$("button").prop("disabled", true);
```

### Change Text Inside an Element Using jQuery
The <<span style = color:red>.html()</span> function will add HTML text and tags w/in an element.
```JavaScript
$("h3").html("<em>New Text</em>");
```

### Remove an Element Using jQuery
Use <span style = color:red>.remove()</span> to remove element(s).
```JavaScript
$("#soup").remove()
//No #soup for you!
```

### Use appendTo to Move Elements with jQuery
You can move an element from one div to another w/ <span style = color:red>.appendTo()</span>.
```JavaScript
$("#rightWellWords").appendTo("#left-well")
```
### Clone an Element Using jQuery
In the example above, we moved an element from one div to another.  If, instead, we wanted to make a copy and move that copy, we would use:
```JavaScript
$("#rightWellWords").clone().appendTo("#left-well")
```
The function <span style = color:red>.clone()</span> makes the copy and is chained together w/ <span style = color:red>.appendTo()</span>.  This is called function chaining.

### Target the Parent of an Element Using jQuery
To target the parent element of an element, use <span style = color:red>.parent()</span>.  For example, to change a background color of all <p> text:
```JavaScript
$("p").parent().css("background-color, blue")
```

### Target the Children of an Element Using jQuery
Similarly, one can target the children of a parent element w/ <span style = color:red>.children()</span>:
```JavaScript
$("#left-well").children().css("color, gray")
```

### Target a Specific Child of an Element Using jQuery
To target one child, as opposed to all children, of a parent element, use <span style = color:red>target:nth-child(n)</span>
```JavaScript
$("#left-well:nth-child(2)").css("color, blue")
```

### Target Even or Odd Elements Using jQuery
To target even or odd elements, use <span style = color:red>:even</span> or <span style = color:red>:odd</span>.
```JavaScript
$(".target:odd").addClass("shake")
```
For example, if we have classes <span style = color:red>target1</span> and <span style = color:red>target2</span>,<span style = color:red> target1</span> will now be shaking.

### Use jQuery to Modify the Entire Page
To target the whole page, target the <span style = color:red>body</span> element.
```JavaScript
$("body").addClass("animated bounce")
```
