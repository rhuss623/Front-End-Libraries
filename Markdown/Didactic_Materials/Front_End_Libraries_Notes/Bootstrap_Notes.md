<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous"/>

# Bootstrap Notes
Hi! My name is Ryan Hussey and these are my personal notes for freeCodeCamp's Bootstrap lessons.<br>Feel free to use them if they are useful to you.

To initiate bootstrap, start your file with the following:
```HTML
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous"/>
```
Nest the HTML (w/ the exception of <link>) in:
```HTML
<div class = container-fluid></div>
```
### Make Images Mobile Responsive

To make an image's size respond to the width of the screen, use the class <span style = color:red> img-responsive</span>.
```HTML
<img src="https://bit.ly/fcc-running-cats" class=img-responsive>
```
<img src="https://bit.ly/fcc-running-cats" class=img-responsive>

### Center Text

```HTML
<h2 class="text-center">Centered Text</h2>
```
<h2 class="red-text text-center">Centered Text</h2>

### Button
```HTML
<button class = "btn btn-default">Button</button>
```
<button class = "btn btn-default">Button</button>

### Block Elements
Block Elements Stretch to fit the width of the page.
```HTML
```
<button class="btn btn-default btn-block">Block Element Button</button>

### Primary
The primary class is the main color you'll use in your app.
```HTML
<button class="btn btn-primary btn-block">Primary Class Button</button>
```
<button class="btn btn-primary btn-block">Primary Class Button</button>

### Call out Optional Actions with btn-info

Bootstrap comes with several colors built in for buttons. See the options with btn-info.
```HTML
<button class="btn btn-primary btn-block btn-info">Primary Button w/ btn-info class</button>
<button class="btn btn-default btn-block btn-info">Primary Button w/ btn-info class</button>
```
<button class="btn btn-primary btn-block">Primary Button w/ btn-info class</button>
<button class="btn btn-default btn-block btn-info">Default Button w/ btn-info class</button>

### Warn Your Users of a Dangerous Action with btn-danger
```HTML
<button class="btn btn-default btn-block btn-danger">I am a Dangerous Button</button>
```

### Use the Bootstrap Grid to Put Elements Side By Side

Bootstrap has a built in 12 column grid.  To designate the grid size and number of columns, apply this template of class to your element:<br>
col-sizeHere-widthHere<br>
Size options are to be chosen based on screen width: <br>
xs — screen width < 576px (This is the “default” tier)
sm — screen width ≥ 576px.
md — screen width ≥ 768px.
lg — screen width ≥ 992px.
xl — screen width ≥ 1200px.<br>
source = https://uxplanet.org/how-the-bootstrap-4-grid-works-a1b04703a3b7
<br> "widthHere" is the number of columns your element should inhabit.
<br>
To designate a row, nest all elements in the row in:
```HTML
<div class="row"></div>
```
and then nest each individual element in:
```HTML
<div class="col-sizeHere-widthHere"></div>
```
for example:
```HTML
<div class="row">
<div class="col-xs-4">
  <button class="btn btn-default btn-block">Default</button>
</div>
<div class="col-xs-4">
  <button class="btn btn-primary btn-block">Primary</button>
</div>
<div class="col-xs-4">
  <button class="btn btn-default btn-info btn-block">Default</button>
</div>
</div>
```
<div class="row">
<div class="col-xs-4">
  <button class="btn btn-default btn-block">Default</button>
</div>
<div class="col-xs-4">
  <button class="btn btn-primary btn-block">Primary</button>
</div>
<div class="col-xs-4">
  <button class="btn btn-default btn-info btn-block">Default</button>
</div>
</div>
### Use a span to Target Inline Elements

You can use span to put elements in the same line and/or style inline elements.
e.g.
```HTML
<p>This word is <span class="text-danger">dangerous</span>!</p>
```
<p>This word is <span class="text-danger">dangerous</span>!</p>

### Add Font Awesome Icons to our Buttons

First, add the following to your file:
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.5.0/css/font-awesome.min.css" integrity="sha384-XdYbMnZ/QjLh6iI4ogqCTaIjrFk87ip+ekIjefZch0Y+PvJ8CDYtEs1ipDmPorQ+" crossorigin="anonymous">
```HTML
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.5.0/css/font-awesome.min.css" integrity="sha384-XdYbMnZ/QjLh6iI4ogqCTaIjrFk87ip+ekIjefZch0Y+PvJ8CDYtEs1ipDmPorQ+" crossorigin="anonymous">
```
Either use <span style=color:red>span</span> or<span style=color:red> i</span> element to add Font Awesome (fa).  You can specify the size using pixels or they will automatically inherit the size of their parent element.
```HTML
<i class="fa fa-info-circle"></i>
<span class="fas fa-ambulance"></span>
```
For a gallery of Font Awesome icons, visit:<br> <a href="https://fontawesome.com/icons?d=gallery" target=blank>Font Awesome</a>

### Well Divs
Well Divs are a pretty way to house elements.
```HTML
 <div class="well"></div>
 ```

 ### Classes v. ID's
 Classes aren't only used for css styling, they can be useful for creating targets for selection.  

 When targeting multiple elements at once, use class attribute.  <br>
 ID attributes should be unique to one element and one element only.

 ### Commenting HTML That Shouldn't be Touched

 When using JQuery to edit HTML, the original HTML doesn't need to be touched and should be designated as such w/ a comment, e.g.:
 ```HTML
 <!-- Only change code above this line. -->
 ```

 ## Resources:
 <a href = "https://www.w3schools.com/bootstrap/bootstrap_ref_all_classes.asp" target = blank>Here's a link to all Bootstrap CSS classes</a>
