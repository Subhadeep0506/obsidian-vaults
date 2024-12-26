# Bootstrap

## 1. Use Responsive Design with Bootstrap Fluid Containers
In the HTML5 and CSS section of freeCodeCamp we built a Cat Photo App. Now let's go back to it. This time, we'll style it using the popular Bootstrap responsive CSS framework.

Bootstrap will figure out how wide your screen is and respond by resizing your HTML elements - hence the name responsive design.

With responsive design, there is no need to design a mobile version of your website. It will look good on devices with screens of any width.

You can add Bootstrap to any app by adding the following code to the top of your HTML:

```html
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous"/>
```

In this case, we've already added it for you to this page behind the scenes. Note that using either `>` or `/>` to close the `link` tag is acceptable.

To get started, we should nest all of our HTML (except the `link` tag and the `style` element) in a `div` element with the class `container-fluid`.

### Solution:
```html
<link href="https://fonts.googleapis.com/css?family=Lobster" rel="stylesheet" type="text/css">
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous"/>
<style>
.red-text {
	color: red;
}
h2 {
	font-family: Lobster, Monospace;
}
p {
	font-size: 16px;
	font-family: Monospace;
}
.thick-green-border {
	border-color: green;
	border-width: 10px;
	border-style: solid;
	border-radius: 50%;
}
.smaller-image {
	width: 100px;
}
</style>
<div class="container-fluid">
	.
	.
	.
</div>
```

## 2. Make Images Mobile Responsive
First, add a new image below the existing one. Set its `src` attribute to `https://cdn.freecodecamp.org/curriculum/cat-photo-app/running-cats.jpg`.

It would be great if this image could be exactly the width of our phone's screen.

Fortunately, with Bootstrap, all we need to do is add the `img-responsive` class to your image. Do this, and the image should perfectly fit the width of your page.

### Solution:
```html
<img class="img-responsive" src="`https://cdn.freecodecamp.org/curriculum/cat-photo-app/running-cats.jpg`">
```

## 3. Center Text with Bootstrap
Now that we're using Bootstrap, we can center our heading element to make it look better. All we need to do is add the class `text-center` to our `h2` element.

Remember that you can add several classes to the same element by separating each of them with a space, like this:

```html
<h2 class="red-text text-center">your text</h2>
```

### Solution:
```html
<h2 class="red-text text-center">CatPhotoApp</h2>
```

## 4. Create a Bootstrap Button
Bootstrap has its own styles for `button` elements, which look much better than the plain HTML ones.
Create a new `button` element below your large kitten photo. Give it the `btn` and `btn-default` classes, as well as the text of `Like`.

### Solution
```html
<button class="btn btn-default">Like</button>
```

## 5. Create a Block Element Bootstrap Button
Normally, your `button` elements with the `btn` and `btn-default` classes are only as wide as the text that they contain. For example:

```html
<button class="btn btn-default">Submit</button>
```

This button would only be as wide as the word `Submit`.

By making them block elements with the additional class of `btn-block`, your button will stretch to fill your page's entire horizontal space and any elements following it will flow onto a "new line" below the block.

```html
<button class="btn btn-default btn-block">Submit</button>
```

This button would take up 100% of the available width.
Note that these buttons still need the `btn` class.
Add Bootstrap's `btn-block` class to your Bootstrap button.

## 6. Taste the Bootstrap Button Color Rainbow
The `btn-primary` class is the main color you'll use in your app. It is useful for highlighting actions you want your user to take.
Replace Bootstrap's `btn-default` class with `btn-primary` in your button.
Note that this button will still need the `btn` and `btn-block` classes.

### Solution:
```html
<button class="btn btn-primary btn-block">Like</button>
```

## 7. Call out Optional Actions with btn-info
Bootstrap comes with several pre-defined colors for buttons. The `btn-info` class is used to call attention to optional actions that the user can take.

Create a new block-level Bootstrap button below your `Like` button with the text `Info`, and add Bootstrap's `btn-info` class to it.

Note that these buttons still need the `btn` and `btn-block` classes.

### Solution
```html
<button class="btn btn-block btn-info">Info</button>
```

## 8. Warn Your Users of a Dangerous Action with btn-danger
Bootstrap comes with several pre-defined colors for buttons. The `btn-danger` class is the button color you'll use to notify users that the button performs a destructive action, such as deleting a cat photo.

Create a button with the text `Delete` and give it the class `btn-danger`.

Note that these buttons still need the `btn` and `btn-block` classes.

### Source
```html
<button class="btn btn-block btn-danger">Delete</button>
```

## 9. Use the Bootstrap Grid to Put Elements Side By Side
Bootstrap uses a responsive 12-column grid system, which makes it easy to put elements into rows and specify each element's relative width. Most of Bootstrap's classes can be applied to a `div` element.

Bootstrap has different column width attributes that it uses depending on how wide the user's screen is. For example, phones have narrow screens, and laptops have wider screens.

Take for example Bootstrap's `col-md-*` class. Here, `md` means medium, and `*` is a number specifying how many columns wide the element should be. In this case, the column width of an element on a medium-sized screen, such as a laptop, is being specified.

In the Cat Photo App that we're building, we'll use `col-xs-*`, where `xs` means extra small (like an extra-small mobile phone screen), and `*` is the number of columns specifying how many columns wide the element should be.

Put the `Like`, `Info` and `Delete` buttons side-by-side by nesting all three of them within one `<div class="row">` element, then each of them within a `<div class="col-xs-4">` element.

The `row` class is applied to a `div`, and the buttons themselves can be nested within it.

### Solution:
```html
<div class="row">
	<div class="col-xs-4">
		<button class="btn btn-block btn-primary">Like</button>
	</div>
	<div class="col-xs-4">
		<button class="btn btn-block btn-info">Info</button>
	</div>
	<div class="col-xs-4">
		<button class="btn btn-block btn-danger">Delete</button>
	</div>
</div>
```

## 10. Ditch Custom CSS for Bootstrap
We can clean up our code and make our Cat Photo App look more conventional by using Bootstrap's built-in styles instead of the custom styles we created earlier.

Don't worry - there will be plenty of time to customize our CSS later.

Delete the `.red-text`, `p`, and `.smaller-image` CSS declarations from your `style` element so that the only declarations left in your `style` element are `h2` and `thick-green-border`.

Then delete the `p` element that contains a dead link. Then remove the `red-text` class from your `h2` element and replace it with the `text-primary` Bootstrap class.

Finally, remove the `smaller-image` class from your first `img` element and replace it with the `img-responsive` class.

## 11. Use a span to Target Inline Elements
You can use spans to create inline elements. Remember when we used the `btn-block` class to make the button fill the entire row?

That illustrates the difference between an "inline" element and a "block" element.

By using the inline `span` element, you can put several elements on the same line, and even style different parts of the same line differently.

Using a `span` element, nest the word `love` inside the `p` element that currently has the text `Things cats love`. Then give the `span` the class `text-danger` to make the text red.

Here's how you would do this for the `p` element that has the text `Top 3 things cats hate`:

```html
<p>Top 3 things cats <span class="text-danger">hate:</span></p>
```

## 12. Create a Custom Heading
We will make a simple heading for our Cat Photo App by putting the title and relaxing cat image in the same row.

Remember, Bootstrap uses a responsive grid system, which makes it easy to put elements into rows and specify each element's relative width. Most of Bootstrap's classes can be applied to a `div` element.

Nest your first image and your `h2` element within a single `<div class="row">` element. Nest your `h2` element within a `<div class="col-xs-8">` and your image in a `<div class="col-xs-4">` so that they are on the same line.

Notice how the image is now just the right size to fit along the text?

### Solution:
```html
<div class="row">
	<div class="col-xs-8">
		<h2 class="text-primary text-center">CatPhotoApp</h2>
	</div>
	<div class="col-xs-4">
		<a href="#">
			<img class="img-responsive thick-green-border" src="https://cdn.freecodecamp.org/curriculum/cat-photo-app/relaxing-cat.jpg" alt="A cute orange cat lying on its back.">
		</a>
	</div>
</div>
```

## 13. Add Font Awesome Icons to our Buttons
Font Awesome is a convenient library of icons. These icons can be webfonts or vector graphics. These icons are treated just like fonts. You can specify their size using pixels, and they will assume the font size of their parent HTML elements.

You can include Font Awesome in any app by adding the following code to the top of your HTML:

```html
<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.8.1/css/all.css" integrity="sha384-50oBUHEmvpQ+1lW4y57PTFmhCaXp0ML5d60M1M7uH2+nqUivzIebhndOJK28anvf" crossorigin="anonymous">
```

In this case, we've already added it for you to this page behind the scenes.

The `i` element was originally used to make other elements italic, but is now commonly used for icons. You can add the Font Awesome classes to the `i` element to turn it into an icon, for example:

```html
<i class="fas fa-info-circle"></i>
```

Note that the `span` element is also acceptable for use with icons.

Use Font Awesome to add a `thumbs-up` icon to your like button by giving it an `i` element with the classes `fas` and `fa-thumbs-up`. Make sure to keep the text `Like` next to the icon.

### Solution:
```html
<button class="btn btn-block btn-primary">
	<i class="fas fa-thumbs-up"> Like</i>
</button>
```

## 14. Add Font Awesome Icons to all of our Buttons
Font Awesome is a convenient library of icons. These icons can be web fonts or vector graphics. These icons are treated just like fonts. You can specify their size using pixels, and they will assume the font size of their parent HTML elements.

Use Font Awesome to add an `info-circle` icon to your info button and a `trash` icon to your delete button.

**Note:** The `span` element is an acceptable alternative to the `i` element for the directions below.

### Solution:
```html
<button class="btn btn-block btn-info"><i class="fas fa-info-circle"> Info</i></button>
<button class="btn btn-block btn-danger"><i class="fas fa-trash"> Delete</i></button>
```

## 15. Responsively Style Radio Buttons
You can use Bootstrap's `col-xs-*` classes on `form` elements, too! This way, our radio buttons will be evenly spread out across the page, regardless of how wide the screen resolution is.

Nest both your radio buttons within a `<div class="row">` element. Then nest each of them within a `<div class="col-xs-6">` element.

**Note:** As a reminder, radio buttons are `input` elements of type `radio`.

### Solution:
```html
<div class="row">
	<div class="col-xs-6">
		<label><input type="radio" name="indoor-outdoor"> Indoor</label>
	</div>
	<div class="col-xs-6">
		<label><input type="radio" name="indoor-outdoor"> Outdoor</label>
	</div>
</div>
```

## 16. Responsively Style Checkboxes
Since Bootstrap's `col-xs-*` classes are applicable to all `form` elements, you can use them on your checkboxes too! This way, the checkboxes will be evenly spread out across the page, regardless of how wide the screen resolution is.

Nest all three of your checkboxes in a `<div class="row">` element. Then nest each of them in a `<div class="col-xs-4">` element.

## 17. Style Text Inputs as Form Controls
You can add the `fa-paper-plane` Font Awesome icon by adding `<i class="fa fa-paper-plane"></i>` within your submit `button` element.

Give your form's text input field a class of `form-control`. Give your form's submit button the classes `btn btn-primary`. Also give this button the Font Awesome icon of `fa-paper-plane`.

All textual `<input>`, `<textarea>`, and `<select>` elements with the class `.form-control` have a width of 100%.

### Solution:
```html
<input class="form-control" type="text" placeholder="cat photo URL" required>

<button class="btn btn-primary" type="submit">
	<i class="fa fa-paper-plane"> Submit</i>
</button>
```

## 18. Line up Form Elements Responsively with Bootstrap
Now let's get your form `input` and your submission `button` on the same line. We'll do this the same way we have previously: by using a `div` element with the class `row`, and other `div` elements within it using the `col-xs-*` class.

Nest both your form's text `input` and submit `button` within a `div` with the class `row`. Nest your form's text `input` within a div with the class of `col-xs-7`. Nest your form's submit `button` in a `div` with the class `col-xs-5`.

This is the last challenge we'll do for our Cat Photo App for now. We hope you've enjoyed learning Font Awesome, Bootstrap, and responsive design!

### Solution:
```html
<div class="row">
	<div class="col-xs-7">
		<input type="text" class="form-control" placeholder="cat photo URL" required>
	</div>
	<div class="col-xs-5">
		<button type="submit" class="btn btn-primary"><i class="fa fa-paper-plane"></i> Submit</button>
	</div>
</div>
```

## 19. Create a Bootstrap Headline
Now let's build something from scratch to practice our HTML, CSS and Bootstrap skills.

We'll build a jQuery playground, which we'll soon put to use in our jQuery challenges.

To start with, create an `h3` element, with the text `jQuery Playground`.

Color your `h3` element with the `text-primary` Bootstrap class, and center it with the `text-center` Bootstrap class.

### Solution:
```html
<h3 class="text-primary text-center">jQuery Playground</h3>
```

## 20. House our page within a Bootstrap container-fluid div
Now let's make sure all the content on your page is mobile-responsive.

Let's nest your `h3` element within a `div` element with the class `container-fluid`.

### Solution:
```html
<div class="container-fluid">
	<h3 class="text-primary text-center">jQuery Playground</h3>
</div>
```

## 21. Create a Bootstrap Row
Now we'll create a Bootstrap row for our inline elements.
Create a `div` element below the `h3` tag, with a class of `row`.

## 22. Split Your Bootstrap Row
Now that we have a Bootstrap Row, let's split it into two columns to house our elements.
Create two `div` elements within your row, both with the class `col-xs-6`.

## 23. Create Bootstrap Wells
Bootstrap has a class called `well` that can create a visual sense of depth for your columns.
Nest one `div` element with the class `well` within each of your `col-xs-6` `div` elements.

## 24. Add Elements within Your Bootstrap Wells
Now we're several `div` elements deep on each column of our row. This is as deep as we'll need to go. Now we can add our `button` elements.
Nest three `button` elements within each of your `div` elements having the class name `well`.

## 25. Create a Class to Target with jQuery Selectors
Not every class needs to have corresponding CSS. Sometimes we create classes just for the purpose of selecting these elements more easily using jQuery.

Give each of your `button` elements the class `target`.

### Solution:
```html
<div class="row">
	<div class="col-xs-6">
		<div class="well">
			<button class="btn btn-default target"></button>
			<button class="btn btn-default target"></button>
			<button class="btn btn-default target"></button>
		</div>
	</div>
	<div class="col-xs-6">
		<div class="well">
			<button class="btn btn-default target"></button>
			<button class="btn btn-default target"></button>
			<button class="btn btn-default target"></button>
		</div>
	</div>
</div>
```

## 26. Add id Attributes to Bootstrap Elements
Recall that in addition to class attributes, you can give each of your elements an `id` attribute.
Each id must be unique to a specific element and used only once per page.
Let's give a unique id to each of our `div` elements of class `well`.
Remember that you can give an element an id like this:
```html
<div class="well" id="center-well">
```

Give the well on the left the id of `left-well`. Give the well on the right the id of `right-well`.

## 27. Label Bootstrap Wells
For the sake of clarity, let's label both of our wells with their ids.
Above your left-well, inside its `col-xs-6` `div` element, add a `h4` element with the text `#left-well`.
Above your right-well, inside its `col-xs-6` `div` element, add a `h4` element with the text `#right-well`.

## 28. Give Each Element a Unique id
We will also want to be able to use jQuery to target each button by its unique id.
Give each of your buttons a unique id, starting with `target1` and ending with `target6`.
Make sure that `target1` to `target3` are in `#left-well`, and `target4` to `target6` are in `#right-well`.

## 29. Label Bootstrap Buttons
Just like we labeled our wells, we want to label our buttons.
Give each of your `button` elements text that corresponds to its id selector.

### Solution:
```html
<div class="container-fluid">
	<h3 class="text-primary text-center">jQuery Playground</h3>
		<div class="row">
			<div class="col-xs-6">
				<h4>#left-well</h4>
				<div class="well" id="left-well">
					<button class="btn btn-default target" id="target1">#target1</button>
					<button class="btn btn-default target" id="target2">#target2</button>
					<button class="btn btn-default target" id="target3">#target3</button>
				</div>
			</div>
			<div class="col-xs-6">
				<h4>#right-well</h4>
				<div class="well" id="right-well">
					<button class="btn btn-default target" id="target4">#target4</button>
					<button class="btn btn-default target" id="target5">#target5</button>
					<button class="btn btn-default target" id="target6">#target6</button>
				</div>
			</div>
		</div>
</div>
```



# jQuery

## 1. Learn How Script Tags and Document Ready Work
Now we're ready to learn jQuery, the most popular JavaScript tool of all time.

Before we can start using jQuery, we need to add some things to our HTML.

First, add a `script` element at the top of your page. Be sure to close it on the following line.

Your browser will run any JavaScript inside a `script` element, including jQuery.

Inside your `script` element, add this code: `$(document).ready(function() {` to your `script`. 

Then close it on the following line (still inside your `script` element) with: `});`

We'll learn more about `functions` later. The important thing to know is that code you put inside this `function` will run as soon as your browser has loaded your page.

This is important because without your `document ready function`, your code may run before your HTML is rendered, which would cause bugs.

### Solution:
```html
<script>
	$(document).ready(function() {
	
	});
</script>
```

## 2. Target HTML Elements with Selectors Using jQuery
Now we have a `document ready` function.
Now let's write our first jQuery statement. All jQuery functions start with a `$`, usually referred to as a dollar sign operator, or as bling.

jQuery often selects an HTML element with a selector, then does something to that element.

For example, let's make all of your `button` elements bounce. Just add this code inside your document ready function:

```js
$("button").addClass("animated bounce");
```

Note that we've already included both the jQuery library and the Animate.css library in the background so that you can use them in the editor. So you are using jQuery to apply the Animate.css `bounce` class to your `button` elements.

### Solution:
```html
<script>
	$(document).ready(function() {
		$("button").addClass("animated bounce");
	});
</script>
```

## 3. Target Elements by Class Using jQuery
You see how we made all of your `button` elements bounce? We selected them with `$("button")`, then we added some CSS classes to them with `.addClass("animated bounce");`.

You just used jQuery's `.addClass()` function, which allows you to add classes to elements.

First, let's target your `div` elements with the class `well` by using the `$(".well")` selector.

Note that, just like with CSS declarations, you type a `.` before the class's name.

Then use jQuery's `.addClass()` function to add the classes `animated` and `shake`.

For example, you could make all the elements with the class `text-primary` shake by adding the following to your `document ready function`:

```js
$(".text-primary").addClass("animated shake");
```

### Solution:
```html
<script>
	$(document).ready(function() {
		$("button").addClass("animated bounce");
		$(".well").addClass("animated shake");
		$(".text-primary").addClass("animated shake");
	});
</script>
```

## 4. Target Elements by id Using jQuery
You can also target elements by their id attributes.

First target your `button` element with the id `target3` by using the `$("#target3")` selector.

Note that, just like with CSS declarations, you type a `#` before the id's name.

Then use jQuery's `.addClass()` function to add the classes `animated` and `fadeOut`.

Here's how you'd make the `button` element with the id `target6` fade out:

```js
$("#target6").addClass("animated fadeOut");
```

### Solution:
```js
$("#target3").addClass("animated fadeout")
```

## 5. Delete Your jQuery Functions
These animations were cool at first, but now they're getting kind of distracting.

Delete all three of these jQuery functions from your `document ready function`, but leave your `document ready function` itself intact.

## 6. Target the Same Element with Multiple jQuery Selectors
Now you know three ways of targeting elements: by type: `$("button")`, by class: `$(".btn")`, and by id `$("#target1")`.

Although it is possible to add multiple classes in a single `.addClass()` call, let's add them to the same element in _three separate ways_.

Using `.addClass()`, add only one class at a time to the same element, three different ways:

Add the `animated` class to all elements with type `button`.

Add the `shake` class to all the buttons with class `.btn`.

Add the `btn-primary` class to the button with id `#target1`.

**Note:** You should only be targeting one element and adding only one class at a time. Altogether, your three individual selectors will end up adding the three classes `shake`, `animated`, and `btn-primary` to `#target1`.

### Solution:
```html
<script>
	$(document).ready(function() {
		$("button").addClass("animated")
		$(".btn").addClass("shake")
		$("#target1").addClass("btn-primary")
	});
</script>
```

## 7. Remove Classes from an Element with jQuery
In the same way you can add classes to an element with jQuery's `addClass()` function, you can remove them with jQuery's `removeClass()` function.

Here's how you would do this for a specific button:

```js
$("#target2").removeClass("btn-default");
```

Let's remove the `btn-default` class from all of our `button` elements.

## 8. Change the CSS of an Element Using jQuery
We can also change the CSS of an HTML element directly with jQuery.

jQuery has a function called `.css()` that allows you to change the CSS of an element.

Here's how we would change its color to blue:

```js
$("#target1").css("color", "blue");
```

This is slightly different from a normal CSS declaration, because the CSS property and its value are in quotes, and separated with a comma instead of a colon.

Delete your jQuery selectors, leaving an empty `document ready function`.

Select `target1` and change its color to red.

## 9. Disable an Element Using jQuery
You can also change the non-CSS properties of HTML elements with jQuery. For example, you can disable buttons.

When you disable a button, it will become grayed-out and can no longer be clicked.

jQuery has a function called `.prop()` that allows you to adjust the properties of elements.

Here's how you would disable all buttons:

```js
$("button").prop("disabled", true);
```

Disable only the `target1` button.

## 10. Change Text Inside an Element Using jQuery
Using jQuery, you can change the text between the start and end tags of an element. You can even change HTML markup.

jQuery has a function called `.html()` that lets you add HTML tags and text within an element. Any content previously within the element will be completely replaced with the content you provide using this function.

Here's how you would rewrite and emphasize the text of our heading:

```js
$("h3").html("<em>jQuery Playground</em>");
```

jQuery also has a similar function called `.text()` that only alters text without adding tags. In other words, this function will not evaluate any HTML tags passed to it, but will instead treat it as the text you want to replace the existing content with.

Change the button with id `target4` by emphasizing its text.

[View our news article for `<em>`](https://www.freecodecamp.org/news/html-elements-explained-what-are-html-tags/#em-element) to learn the difference between `<i>` and `<em>` and their uses.

Note that while the `<i>` tag has traditionally been used to emphasize text, it has since been adopted for use as a tag for icons. The `<em>` tag is now widely accepted as the tag for emphasis. Either will work for this challenge.

### Solution:
```html
<script>
	$(document).ready(function() {
		$("#target1").css("color", "red");
		$("#target4").html("<em>#target4</em>")
	});
</script>
```

## 11. Remove an Element Using jQuery
Now let's remove an HTML element from your page using jQuery.

jQuery has a function called `.remove()` that will remove an HTML element entirely

Remove the `#target4` element from the page by using the `.remove()` function.

### Solution:
```html
<script>
	$(document).ready(function() {
		$("#target1").css("color", "red");
		$("#target1").prop("disabled", true);
		$("#target4").remove()
	});
</script>
```

## 12. Use appendTo to Move Elements with jQuery
Now let's try moving elements from one `div` to another.

jQuery has a function called `appendTo()` that allows you to select HTML elements and append them to another element.
For example, if we wanted to move `target4` from our right well to our left well, we would use:
```js
$("#target4").appendTo("#left-well");
```

Move your `target2` element from your `left-well` to your `right-well`.

### Solution:
```html
<script>
	$(document).ready(function() {
		$("#target2").appendTo("#right-well")
	});
</script>
```

## 13. Clone an Element Using jQuery
In addition to moving elements, you can also copy them from one place to another.
jQuery has a function called `clone()` that makes a copy of an element.
For example, if we wanted to copy `target2` from our `left-well` to our `right-well`, we would use:
```js
$("#target2").clone().appendTo("#right-well");
```

Did you notice this involves sticking two jQuery functions together? This is called function chaining and it's a convenient way to get things done with jQuery.

Clone your `target5` element and append it to your `left-well`.

### Solution:
```html
<script>
	$(document).ready(function() {
		$("#target5").clone().appendTo("#left-well")
	});
</script>
```

## 14. Target the Parent of an Element Using jQuery
Every HTML element has a `parent` element from which it `inherits` properties.

For example, your `jQuery Playground` `h3` element has the parent element of `<div class="container-fluid">`, which itself has the parent `body`.
jQuery has a function called `parent()` that allows you to access the parent of whichever element you've selected.
Here's an example of how you would use the `parent()` function if you wanted to give the parent element of the `left-well` element a background color of blue:
```js
$("#left-well").parent().css("background-color", "blue")
```

Give the parent of the `#target1` element a background-color of red.

### Solution:
```js
$("#target1").parent().css("background-color", "red")
```

## 15. Target the Children of an Element Using jQuery
When HTML elements are placed one level below another they are called children of that element. For example, the button elements in this challenge with the text `#target1`, `#target2`, and `#target3` are all children of the `<div class="well" id="left-well">` element.

jQuery has a function called `children()` that allows you to access the children of whichever element you've selected.

Here's an example of how you would use the `children()` function to give the children of your `left-well` element the color `blue`:

```js
$("#left-well").children().css("color", "blue")
```

Give all the children of your `right-well` element the color orange.

### Solution:
```js
$("#right-well").children().css("color", "orange");
```

## 16. Target a Specific Child of an Element Using jQuery
You've seen why id attributes are so convenient for targeting with jQuery selectors. But you won't always have such neat ids to work with.

Fortunately, jQuery has some other tricks for targeting the right elements.

jQuery uses CSS Selectors to target elements. The `target:nth-child(n)` CSS selector allows you to select all the nth elements with the target class or element type.

Here's how you would give the third element in each well the bounce class:
```js
$(".target:nth-child(3)").addClass("animated bounce");
```

Make the second child in each of your well elements bounce. You must select the elements' children with the `target` class.

### Solution:
```js
$(".target:nth-child(2)").addClass("animated bounce")
```

## 17. Target Even Elements Using jQuery
You can also target elements based on their positions using `:odd` or `:even` selectors.

Note that jQuery is zero-indexed which means the first element in a selection has a position of 0. This can be a little confusing as, counter-intuitively, `:odd` selects the second element (position 1), fourth element (position 3), and so on.

Here's how you would target all the odd elements with class `target` and give them classes:
```js
$(".target:odd").addClass("animated shake");
```

Try selecting all the even `target` elements and giving them the classes of `animated` and `shake`. Remember that **even** refers to the position of elements with a zero-based system in mind.

### Solution:
```js
$(".target:even").addClass("animated shake")
```

## 18. Use jQuery to Modify the Entire Page
We're done playing with our jQuery playground. Let's tear it down!
jQuery can target the `body` element as well.
Here's how we would make the entire body fade out: `$("body").addClass("animated fadeOut");`

But let's do something more dramatic. Add the classes `animated` and `hinge` to your `body` element.

### Solution:
```js
$("body").addClass("animated hinge")
```

# SASS

## 1. Store Data with Sass Variables
One feature of Sass that's different than CSS is it uses variables. They are declared and set to store data, similar to JavaScript.

In JavaScript, variables are defined using the `let` and `const` keywords. In Sass, variables start with a `$` followed by the variable name.

Here are a couple examples:

```scss
$main-fonts: Arial, sans-serif;
$headings-color: green;
```

And to use the variables:

```scss
h1 {
  font-family: $main-fonts;
  color: $headings-color;
}
```

One example where variables are useful is when a number of elements need to be the same color. If that color is changed, the only place to edit the code is the variable value.

Create a variable `$text-color` and set it to `red`. Then change the value of the `color` property for the `.blog-post` and `h2` to the `$text-color` variable.

### Solution:
```scss
<style type='text/scss'>
	$text-color: red;
	.header{
		text-align: center;
	}
	.blog-post, h2 {
		color: $text-color;
	}
</style>
```

## 2. Nest CSS with Sass
Sass allows nesting of CSS rules, which is a useful way of organizing a style sheet.

Normally, each element is targeted on a different line to style it, like so:
```scss
nav {
  background-color: red;
}
nav ul {
  list-style: none;
}
nav ul li {
  display: inline-block;
}
```

For a large project, the CSS file will have many lines and rules. This is where nesting can help organize your code by placing child style rules within the respective parent elements:

```scss
nav {
  background-color: red;
  ul {
    list-style: none;
    li {
      display: inline-block;
    }
  }
}
```

Use the nesting technique shown above to re-organize the CSS rules for both children of `.blog-post` element. For testing purposes, the `h1` should come before the `p` element.

### Solution:
```scss
.blog-post {
	h1 {
		text-align: center;
		color: blue;
	}
	p {
		font-size: 20px;
	}
}
```

## 3. Create Reusable CSS with Mixins
In Sass, a mixin is a group of CSS declarations that can be reused throughout the style sheet.

Newer CSS features take time before they are fully adopted and ready to use in all browsers. As features are added to browsers, CSS rules using them may need vendor prefixes. Consider `box-shadow`:

```scss
div {
  -webkit-box-shadow: 0px 0px 4px #fff;
  -moz-box-shadow: 0px 0px 4px #fff;
  -ms-box-shadow: 0px 0px 4px #fff;
  box-shadow: 0px 0px 4px #fff;
}
```

It's a lot of typing to re-write this rule for all the elements that have a `box-shadow`, or to change each value to test different effects. Mixins are like functions for CSS. Here is how to write one:

```scss
@mixin box-shadow($x, $y, $blur, $c){ 
  -webkit-box-shadow: $x $y $blur $c;
  -moz-box-shadow: $x $y $blur $c;
  -ms-box-shadow: $x $y $blur $c;
  box-shadow: $x $y $blur $c;
}
```

The definition starts with `@mixin` followed by a custom name. The parameters (the `$x`, `$y`, `$blur`, and `$c` in the example above) are optional. Now any time a `box-shadow` rule is needed, only a single line calling the mixin replaces having to type all the vendor prefixes. A mixin is called with the `@include` directive:

```scss
div {
  @include box-shadow(0px, 0px, 4px, #fff);
}
```

Write a mixin for `border-radius` and give it a `$radius` parameter. It should use all the vendor prefixes from the example. Then use the `border-radius` mixin to give the `#awesome` element a border radius of `15px`.

### Solution:

```scss
@mixin border-radius($radius) {
	-webkit-border-radius: $radius;
	-moz-border-radius: $radius;
	-ms-border-radius: $radius;
	border-radius: $radius;
}
#awesome {
	width: 150px;
	height: 150px;
	background-color: green;
	@include border-radius(15px);
}
```

## 4. Use @if and @else to Add Logic To Your Styles
The `@if` directive in Sass is useful to test for a specific case - it works just like the `if` statement in JavaScript.

```scss
@mixin make-bold($bool) {
  @if $bool == true {
    font-weight: bold;
  }
}
```

And just like in JavaScript, `@else if` and `@else` test for more conditions:

```scss
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

Create a mixin called `border-stroke` that takes a parameter `$val`. The mixin should check for the following conditions using `@if`, `@else if`, and `@else`:

```scss
light - 1px solid black
medium - 3px solid black
heavy - 6px solid black
```

If `$val` is not `light`, `medium`, or `heavy`, the border should be set to `none`.

### Solution:
```scss
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
```

## 5. Use **@for** to Create a Sass Loop
The `@for` directive adds styles in a loop, very similar to a `for` loop in JavaScript.

`@for` is used in two ways: "start through end" or "start to end". The main difference is that the "start **to** end" _excludes_ the end number as part of the count, and "start **through** end" _includes_ the end number as part of the count.

Here's a start **through** end example:
```scss
@for $i from 1 through 12 {
  .col-#{$i} { width: 100%/12 * $i; }
}
```

The `#{$i}` part is the syntax to combine a variable (`i`) with text to make a string. When the Sass file is converted to CSS, it looks like this:
```scss
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
```

This is a powerful way to create a grid layout. Now you have twelve options for column widths available as CSS classes.

Write a `@for` directive that takes a variable `$j` that goes from 1 **to** 6.

It should create 5 classes called `.text-1` to `.text-5` where each has a `font-size` set to 15px multiplied by the index

### Solution:

```scss
@for $i from 1 through 6 {
	.text-#{$i} {
		font-size: 15 * $i;
	}
}
```

## 6. Use **@each** to Map Over Items in a List
The last challenge showed how the `@for` directive uses a starting and ending value to loop a certain number of times. Sass also offers the `@each` directive which loops over each item in a list or map. On each iteration, the variable gets assigned to the current value from the list or map.

```scss
@each $color in blue, red, green {
  .#{$color}-text {color: $color;}
}
```

A map has slightly different syntax. Here's an example:

```scss
$colors: (color1: blue, color2: red, color3: green);

@each $key, $color in $colors {
  .#{$color}-text {color: $color;}
}
```

Note that the `$key` variable is needed to reference the keys in the map. Otherwise, the compiled CSS would have `color1`, `color2`... in it. Both of the above code examples are converted into the following CSS:

```scss
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

Write an `@each` directive that goes through a list: `blue, black, red` and assigns each variable to a `.color-bg` class, where the `color` part changes for each item. Each class should set the `background-color` the respective color.

### Solution:
```scss
@each $color in blue, black, red {
	.#{$color}-bg {
		background-color: $color;
	}
}
div {
	height: 200px;
	width: 200px;
}
```

## 7. Apply a Style Until a Condition is Met with **@while**
The `@while` directive is an option with similar functionality to the JavaScript `while` loop. It creates CSS rules until a condition is met.

The `@for` challenge gave an example to create a simple grid system. This can also work with `@while`.

```scss
$x: 1;
@while $x < 13 {
  .col-#{$x} { width: 100%/12 * $x;}
  $x: $x + 1;
}
```

First, define a variable `$x` and set it to 1. Next, use the `@while` directive to create the grid system _while_ `$x` is less than 13. After setting the CSS rule for `width`, `$x` is incremented by 1 to avoid an infinite loop.

Use `@while` to create a series of classes with different `font-sizes`.

There should be 5 different classes from `text-1` to `text-5`. Then set `font-size` to `15px` multiplied by the current index number. Make sure to avoid an infinite loop!

### Solution:
```scss
$i: 1;
@while $i <= 5 {
	.text-#{$i} {
		font-size: 15 * $i;
	}
	$i: $i + 1;
}
```

## 8. Split Your Styles into Smaller Chunks with Partials
Partials in Sass are separate files that hold segments of CSS code. These are imported and used in other Sass files. This is a great way to group similar code into a module to keep it organized.

Names for partials start with the underscore (`_`) character, which tells Sass it is a small segment of CSS and not to convert it into a CSS file. Also, Sass files end with the `.scss` file extension. To bring the code in the partial into another Sass file, use the `@import` directive.

For example, if all your mixins are saved in a partial named "_mixins.scss", and they are needed in the "main.scss" file, this is how to use them in the main file:

```scss
@import 'mixins'
```

Note that the underscore and file extension are not needed in the `import` statement - Sass understands it is a partial. Once a partial is imported into a file, all variables, mixins, and other code are available to use.

Write an `@import` statement to import a partial named `_variables.scss` into the main.scss file.

### Solution:
```scss
<style type="style/scss">
	@import "variables";
</style>
```

## 9. Extend One Set of CSS Styles to Another Element
Sass has a feature called `extend` that makes it easy to borrow the CSS rules from one element and build upon them in another.

For example, the below block of CSS rules style a `.panel` class. It has a `background-color`, `height` and `border`.

```scss
.panel{
  background-color: red;
  height: 70px;
  border: 2px solid green;
}
```

Now you want another panel called `.big-panel`. It has the same base properties as `.panel`, but also needs a `width` and `font-size`. It's possible to copy and paste the initial CSS rules from `.panel`, but the code becomes repetitive as you add more types of panels. The `extend` directive is a simple way to reuse the rules written for one element, then add more for another:

```scss
.big-panel{
  @extend .panel;
  width: 150px;
  font-size: 2em;
}
```

The `.big-panel` will have the same properties as `.panel` in addition to the new styles.

Make a class `.info-important` that extends `.info` and also has a `background-color` set to magenta.

## Solution:
```scss
.info-important {
	@extend .info;
	background-color: magenta;
}
```

# ReactJS

## 1. Create a Simple JSX Element
React is an Open Source view library created and maintained by Facebook. It's a great tool to render the User Interface (UI) of modern web applications.

React uses a syntax extension of JavaScript called JSX that allows you to write HTML directly within JavaScript. This has several benefits. It lets you use the full programmatic power of JavaScript within HTML, and helps to keep your code readable. For the most part, JSX is similar to the HTML that you have already learned, however there are a few key differences that will be covered throughout these challenges.

For instance, because JSX is a syntactic extension of JavaScript, you can actually write JavaScript directly within JSX. To do this, you simply include the code you want to be treated as JavaScript within curly braces: `{ 'this is treated as JavaScript code' }`. Keep this in mind, since it's used in several future challenges.

However, because JSX is not valid JavaScript, JSX code must be compiled into JavaScript. The transpiler Babel is a popular tool for this process. For your convenience, it's already added behind the scenes for these challenges. If you happen to write syntactically invalid JSX, you will see the first test in these challenges fail.

It's worth noting that under the hood the challenges are calling `ReactDOM.render(JSX, document.getElementById('root'))`. This function call is what places your JSX into React's own lightweight representation of the DOM. React then uses snapshots of its own DOM to optimize updating only specific parts of the actual DOM.

The current code uses JSX to assign a `div` element to the constant `JSX`. Replace the `div` with an `h1` element and add the text `Hello JSX!` inside it.

### Solution:
```jsx
const JSX = <h1>Hello JSX!</h1>;
```

## 2. Create a Complex JSX Element
The last challenge was a simple example of JSX, but JSX can represent more complex HTML as well.

One important thing to know about nested JSX is that it must return a single element.

This one parent element would wrap all of the other levels of nested elements.

For instance, several JSX elements written as siblings with no parent wrapper element will not transpile.

Here's an example:

**Valid JSX:**

```jsx
<div>
  <p>Paragraph One</p>
  <p>Paragraph Two</p>
  <p>Paragraph Three</p>
</div>
```

**Invalid JSX:**

```jsx
<p>Paragraph One</p>
<p>Paragraph Two</p>
<p>Paragraph Three</p>
```

---

Define a new constant `JSX` that renders a `div` which contains the following elements in order:

An `h1`, a `p`, and an unordered list that contains three `li` items. You can include any text you want within each element.

**Note:** When rendering multiple elements like this, you can wrap them all in parentheses, but it's not strictly required. Also notice this challenge uses a `div` tag to wrap all the child elements within a single parent element. If you remove the `div`, the JSX will no longer transpile. Keep this in mind, since it will also apply when you return JSX elements in React components.

### Solution:
```JSX
const JSX = (
	<div>
		<h1>Header</h1>
		<p>Paragraph</p>
		<ul>
			<li>item 1</li>
			<li>item 2</li>
			<li>item 3</li>
		</ul>
	</div>
)
```

## 3. Add Comments in JSX
JSX is a syntax that gets compiled into valid JavaScript. Sometimes, for readability, you might need to add comments to your code. Like most programming languages, JSX has its own way to do this.

To put comments inside JSX, you use the syntax `{/* */}` to wrap around the comment text.

The code editor has a JSX element similar to what you created in the last challenge. Add a comment somewhere within the provided `div` element, without modifying the existing `h1` or `p` elements.

### Solution:
```jsx
const JSX = (
	<div>
		{/*This is a Comment*/}
		<h1>This is a block of JSX</h1>
		<p>Here's a subtitle</p>
	</div>
);
```

## 4. Render HTML Elements to the DOM
So far, you've learned that JSX is a convenient tool to write readable HTML within JavaScript. With React, we can render this JSX directly to the HTML DOM using React's rendering API known as ReactDOM.

ReactDOM offers a simple method to render React elements to the DOM which looks like this: `ReactDOM.render(componentToRender, targetNode)`, where the first argument is the React element or component that you want to render, and the second argument is the DOM node that you want to render the component to.

As you would expect, `ReactDOM.render()` must be called after the JSX element declarations, just like how you must declare variables before using them.

The code editor has a simple JSX component. Use the `ReactDOM.render()` method to render this component to the page. You can pass defined JSX elements directly in as the first argument and use `document.getElementById()` to select the DOM node to render them to. There is a `div` with `id='challenge-node'` available for you to use. Make sure you don't change the `JSX` constant.

### Solution:
```jsx
const JSX = (
	<div>
		<h1>Hello World</h1>
		<p>Lets render this to the DOM</p>
	</div>
);
// Change code below this line
ReactDOM.render(JSX, document.getElementById("challenge-node"))
```

## 5. Define an HTML Class in JSX
Now that you're getting comfortable writing JSX, you may be wondering how it differs from HTML.

So far, it may seem that HTML and JSX are exactly the same.

One key difference in JSX is that you can no longer use the word `class` to define HTML classes. This is because `class` is a reserved word in JavaScript. Instead, JSX uses `className`.

In fact, the naming convention for all HTML attributes and event references in JSX become camelCase. For example, a click event in JSX is `onClick`, instead of `onclick`. Likewise, `onchange` becomes `onChange`. While this is a subtle difference, it is an important one to keep in mind moving forward.

Apply a class of `myDiv` to the `div` provided in the JSX code.

### Solution:
```jsx
const JSX = (
	<div className="myDiv">
		<h1>Add a class to this div</h1>
	</div>
);
```

## 6. Learn About Self-Closing JSX Tags
So far, you’ve seen how JSX differs from HTML in a key way with the use of `className` vs. `class` for defining HTML classes.

Another important way in which JSX differs from HTML is in the idea of the self-closing tag.

In HTML, almost all tags have both an opening and closing tag: `<div></div>`; the closing tag always has a forward slash before the tag name that you are closing. However, there are special instances in HTML called “self-closing tags”, or tags that don’t require both an opening and closing tag before another tag can start.

For example the line-break tag can be written as `<br>` or as `<br />`, but should never be written as `<br></br>`, since it doesn't contain any content.

In JSX, the rules are a little different. Any JSX element can be written with a self-closing tag, and every element must be closed. The line-break tag, for example, must always be written as `<br />` in order to be valid JSX that can be transpiled. A `<div>`, on the other hand, can be written as `<div />` or `<div></div>`. The difference is that in the first syntax version there is no way to include anything in the `<div />`. You will see in later challenges that this syntax is useful when rendering React components.

Fix the errors in the code editor so that it is valid JSX and successfully transpiles. Make sure you don't change any of the content - you only need to close tags where they are needed.

### Solution:
```jsx
const JSX = (
	<div>
		<h2>Welcome to React!</h2> <br/ >
		<p>Be sure to close all tags!</p>
		<hr/ >
	</div>
);
```

## 7. Create a Stateless Functional Component
Components are the core of React. Everything in React is a component and here you will learn how to create one.

There are two ways to create a React component. The first way is to use a JavaScript function. Defining a component in this way creates a _stateless functional component_. The concept of state in an application will be covered in later challenges. For now, think of a stateless component as one that can receive data and render it, but does not manage or track changes to that data. (We'll cover the second way to create a React component in the next challenge.)

To create a component with a function, you simply write a JavaScript function that returns either JSX or `null`. One important thing to note is that React requires your function name to begin with a capital letter. Here's an example of a stateless functional component that assigns an HTML class in JSX:

```jsx
const DemoComponent = function() {
  return (
    <div className='customClass' />
  );
};
```

After being transpiled, the `<div>` will have a CSS class of `customClass`.

Because a JSX component represents HTML, you could put several components together to create a more complex HTML page. This is one of the key advantages of the component architecture React provides. It allows you to compose your UI from many separate, isolated components. This makes it easier to build and maintain complex user interfaces.

The code editor has a function called `MyComponent`. Complete this function so it returns a single `div` element which contains some string of text.

**Note:** The text is considered a child of the `div` element, so you will not be able to use a self-closing tag.

### Solution:
```jsx
const MyComponent = function() {
	// Change code below this line
	return (<div>
		Some String
	</div>)
	// Change code above this line
}
```

## 8. Create a React Component
The other way to define a React component is with the ES6 `class` syntax. In the following example, `Kitten` extends `React.Component`:

```jsx
class Kitten extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <h1>Hi</h1>
    );
  }
}
```

This creates an ES6 class `Kitten` which extends the `React.Component` class. So the `Kitten` class now has access to many useful React features, such as local state and lifecycle hooks. Don't worry if you aren't familiar with these terms yet, they will be covered in greater detail in later challenges. Also notice the `Kitten` class has a `constructor` defined within it that calls `super()`. It uses `super()` to call the constructor of the parent class, in this case `React.Component`. The constructor is a special method used during the initialization of objects that are created with the `class` keyword. It is best practice to call a component's `constructor` with `super`, and pass `props` to both. This makes sure the component is initialized properly. For now, know that it is standard for this code to be included. Soon you will see other uses for the constructor as well as `props`.

`MyComponent` is defined in the code editor using class syntax. Finish writing the `render` method so it returns a `div` element that contains an `h1` with the text `Hello React!`.

### Solution:
```jsx
class MyComponent extends React.Component {
	constructor(props) {
		super(props);
	}
	render() {
		return (<div>
			<h1>Hello React!</h1>
			</div>
		)
	}
};
```

## 9. Create a Component with Composition
Now we will look at how we can compose multiple React components together. Imagine you are building an app and have created three components: a `Navbar`, `Dashboard`, and `Footer`.

To compose these components together, you could create an `App` _parent_ component which renders each of these three components as _children_. To render a component as a child in a React component, you include the component name written as a custom HTML tag in the JSX. For example, in the `render` method you could write:

```jsx
return (
 <App>
  <Navbar />
  <Dashboard />
  <Footer />
 </App>
)
```

When React encounters a custom HTML tag that references another component (a component name wrapped in `< />` like in this example), it renders the markup for that component in the location of the tag. This should illustrate the parent/child relationship between the `App` component and the `Navbar`, `Dashboard`, and `Footer`.

In the code editor, there is a simple functional component called `ChildComponent` and a class component called `ParentComponent`. Compose the two together by rendering the `ChildComponent` within the `ParentComponent`. Make sure to close the `ChildComponent` tag with a forward slash.

**Note:** `ChildComponent` is defined with an ES6 arrow function because this is a very common practice when using React. However, know that this is just a function. If you aren't familiar with the arrow function syntax, please refer to the JavaScript section.

### Solution:
```jsx
const ChildComponent = () => {
	return (
		<div>
			<p>I am the child</p>
		</div>
	);
};

class ParentComponent extends React.Component {
	constructor(props) {
		super(props);
	}
	render() {
		return (
			<div>
				<h1>I am the parent</h1>
				<ChildComponent/>
			</div>
		);
	}
};
```

## 10. Use React to Render Nested Components
The last challenge showed a simple way to compose two components, but there are many different ways you can compose components with React.

Component composition is one of React's powerful features. When you work with React, it is important to start thinking about your user interface in terms of components like the App example in the last challenge. You break down your UI into its basic building blocks, and those pieces become the components. This helps to separate the code responsible for the UI from the code responsible for handling your application logic. It can greatly simplify the development and maintenance of complex projects.

There are two functional components defined in the code editor, called `TypesOfFruit` and `Fruits`. Take the `TypesOfFruit` component and compose it, or _nest_ it, within the `Fruits` component. Then take the `Fruits` component and nest it within the `TypesOfFood` component. The result should be a child component, nested within a parent component, which is nested within a parent component of its own!

### Solution:

```jsx
const TypesOfFruit = () => {
	return (
		<div>
			<h2>Fruits:</h2>
			<ul>
				<li>Apples</li>
				<li>Blueberries</li>
				<li>Strawberries</li>
				<li>Bananas</li>
			</ul>
		</div>
	);
};

const Fruits = () => {
	return (
		<div>
			<TypesOfFruit/>
		</div>
	);
};

class TypesOfFood extends React.Component {
	constructor(props) {
		super(props);
	}
	render() {
		return (
			<div>
				<h1>Types of Food:</h1>
				<Fruits/>
			</div>
		);
	}
};
```

## 11. Compose React Components
As the challenges continue to use more complex compositions with React components and `JSX`, there is one important point to note. Rendering `ES6` style class components within other components is no different than rendering the simple components you used in the last few challenges. You can render `JSX` elements, stateless functional components, and `ES6` class components within other components.

In the code editor, the `TypesOfFood` component is already rendering a component called `Vegetables`. Also, there is the `Fruits` component from the last challenge.

Nest two components inside of `Fruits` — first `NonCitrus`, and then `Citrus`. Both of these components are provided for you behind the scenes. Next, nest the `Fruits` class component into the `TypesOfFood` component, below the `h1` heading element and above `Vegetables`. The result should be a series of nested components, which uses two different component types.

### Solution:
```jsx
class Fruits extends React.Component {
	constructor(props) {
		super(props);
	}
	render() {
		return (
			<div>
				<h2>Fruits:</h2>
				<div>
					<Citrus />
					<NonCitrus/>
				</div>
			</div>
		);
	}
};

class TypesOfFood extends React.Component {
	constructor(props) {
		super(props);
	}
	render() {
		return (
			<div>
				<h1>Types of Food:</h1>
				<Fruits/>
				<Vegetables />
			</div>
		);
	}
};
```

## 12. Render a Class Component to the DOM
You may remember using the ReactDOM API in an earlier challenge to render JSX elements to the DOM. The process for rendering React components will look very similar. The past few challenges focused on components and composition, so the rendering was done for you behind the scenes. However, none of the React code you write will render to the DOM without making a call to the ReactDOM API.

Here's a refresher on the syntax: `ReactDOM.render(componentToRender, targetNode)`. The first argument is the React component that you want to render. The second argument is the DOM node that you want to render that component within.

React components are passed into `ReactDOM.render()` a little differently than JSX elements. For JSX elements, you pass in the name of the element that you want to render. However, for React components, you need to use the same syntax as if you were rendering a nested component, for example `ReactDOM.render(<ComponentToRender />, targetNode)`. You use this syntax for both ES6 class components and functional components.

Both the `Fruits` and `Vegetables` components are defined for you behind the scenes. Render both components as children of the `TypesOfFood` component, then render `TypesOfFood` to the DOM. There is a `div` with `id='challenge-node'` available for you to use.

### Solution:
```jsx
class TypesOfFood extends React.Component {
	constructor(props) {
		super(props);
	}
	render() {
		return (
			<div>
				<h1>Types of Food:</h1>
				<Fruits/>
				<Vegetables/>
			</div>
		);
	}
};

ReactDOM.render(<TypesOfFood/>, document.getElementById("challenge-node"))
```

## 13. Write a React Component from Scratch
Now that you've learned the basics of JSX and React components, it's time to write a component on your own. React components are the core building blocks of React applications so it's important to become very familiar with writing them. Remember, a typical React component is an ES6 `class` which extends `React.Component`. It has a render method that returns HTML (from JSX) or `null`. This is the basic form of a React component. Once you understand this well, you will be prepared to start building more complex React projects.

Define a class `MyComponent` that extends `React.Component`. Its render method should return a `div` that contains an `h1` tag with the text: `My First React Component!` in it. Use this text exactly, the case and punctuation matter. Make sure to call the constructor for your component, too.

Render this component to the DOM using `ReactDOM.render()`. There is a `div` with `id='challenge-node'` available for you to use.

### Solution:
```jsx
class MyComponent extends React.Component {
	constructor(props) {
		super(props)
	}
	render() {
		return (
			<div>
				<h1>My First React Component!</h1>
			</div>
		)
	}
}
  
ReactDOM.render(<MyComponent/>, document.getElementById("challenge-node"))
```

## 14. Pass Props to a Stateless Functional Component
The previous challenges covered a lot about creating and composing JSX elements, functional components, and ES6 style class components in React. With this foundation, it's time to look at another feature very common in React: **props**. In React, you can pass props, or properties, to child components. Say you have an `App` component which renders a child component called `Welcome` which is a stateless functional component. You can pass `Welcome` a `user` property by writing:

```jsx
<App>
  <Welcome user='Mark' />
</App>
```

You use **custom HTML attributes** created by you and supported by React to be passed to the component. In this case, the created property `user` is passed to the component `Welcome`. Since `Welcome` is a stateless functional component, it has access to this value like so:

```jsx
const Welcome = (props) => <h1>Hello, {props.user}!</h1>
```

It is standard to call this value `props` and when dealing with stateless functional components, you basically consider it as an argument to a function which returns JSX. You can access the value of the argument in the function body. With class components, you will see this is a little different.

There are `Calendar` and `CurrentDate` components in the code editor. When rendering `CurrentDate` from the `Calendar` component, pass in a property of `date` assigned to the current date from JavaScript's `Date` object. Then access this `prop` in the `CurrentDate` component, showing its value within the `p` tags. Note that for `prop` values to be evaluated as JavaScript, they must be enclosed in curly brackets, for instance `date={Date()}`.

### Solution:
```jsx
const CurrentDate = (props) => {
	return (
		<div>
			<p>The current date is: {props.date}</p>
		</div>
	);
};

class Calendar extends React.Component {
	constructor(props) {
		super(props);
	}
	render() {
		return (
			<div>
				<h3>What date is it?</h3>
				<CurrentDate date={Date()}/>
			</div>
		);
	}
};
```

## 15. Pass an Array as Props
The last challenge demonstrated how to pass information from a parent component to a child component as `props` or properties. This challenge looks at how arrays can be passed as `props`. To pass an array to a JSX element, it must be treated as JavaScript and wrapped in curly braces.

```jsx
<ParentComponent>
  <ChildComponent colors={["green", "blue", "red"]} />
</ParentComponent>
```

The child component then has access to the array property `colors`. Array methods such as `join()` can be used when accessing the property. `const ChildComponent = (props) => <p>{props.colors.join(', ')}</p>` This will join all `colors` array items into a comma separated string and produce: `<p>green, blue, red</p>` Later, we will learn about other common methods to render arrays of data in React.

There are `List` and `ToDo` components in the code editor. When rendering each `List` from the `ToDo` component, pass in a `tasks` property assigned to an array of to-do tasks, for example `["walk dog", "workout"]`. Then access this `tasks` array in the `List` component, showing its value within the `p` element. Use `join(", ")` to display the `props.tasks`array in the `p` element as a comma separated list. Today's list should have at least 2 tasks and tomorrow's should have at least 3 tasks.

### Solution:
```jsx
const List = (props) => {
	return <p>{props.tasks.join(', ')}</p>
};
  
class ToDo extends React.Component {
	constructor(props) {
		super(props);
	}
	render() {
		return (
			<div>
				<h1>To Do Lists</h1>
				<h2>Today</h2>
				<List tasks={["walk dog", "workout"]}/>
				<h2>Tomorrow</h2>
				<List tasks={["walk dog", "workout", "something"]}/>
			</div>
		);
	}
};
```

## 16. Use Default Props
React also has an option to set default props. You can assign default props to a component as a property on the component itself and React assigns the default prop if necessary. This allows you to specify what a prop value should be if no value is explicitly provided. For example, if you declare `MyComponent.defaultProps = { location: 'San Francisco' }`, you have defined a location prop that's set to the string `San Francisco`, unless you specify otherwise. React assigns default props if props are undefined, but if you pass `null` as the value for a prop, it will remain `null`.

The code editor shows a `ShoppingCart` component. Define default props on this component which specify a prop `items` with a value of `0`.

### Solution:
```jsx
const ShoppingCart = (props) => {
	return (
		<div>
			<h1>Shopping Cart Component</h1>
		</div>
	)
};
  
ShoppingCart.defaultProps = {
	items: 0
}
```

## 17. Override Default Props
The ability to set default props is a useful feature in React. The way to override the default props is to explicitly set the prop values for a component.

The `ShoppingCart` component now renders a child component `Items`. This `Items` component has a default prop `quantity` set to the integer `0`. Override the default prop by passing in a value of `10` for `quantity`.

**Note:** Remember that the syntax to add a prop to a component looks similar to how you add HTML attributes. However, since the value for `quantity` is an integer, it won't go in quotes but it should be wrapped in curly braces. For example, `{100}`. This syntax tells JSX to interpret the value within the braces directly as JavaScript.

### Solution:
```jsx
const Items = (props) => {
	return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
}
  
Items.defaultProps = {
	quantity: 0
}
  
class ShoppingCart extends React.Component {
	constructor(props) {
		super(props);
	}
	render() {
		return <Items quantity={10}/>
	}
};
```

## 18. Use **PropTypes** to Define the Props You Expect
React provides useful type-checking features to verify that components receive props of the correct type. For example, your application makes an API call to retrieve data that you expect to be in an array, which is then passed to a component as a prop. You can set `propTypes` on your component to require the data to be of type `array`. This will throw a useful warning when the data is of any other type.

It's considered a best practice to set `propTypes` when you know the type of a prop ahead of time. You can define a `propTypes` property for a component in the same way you defined `defaultProps`. Doing this will check that props of a given key are present with a given type. Here's an example to require the type `function` for a prop called `handleClick`:

```js
MyComponent.propTypes = { handleClick: PropTypes.func.isRequired }
```

In the example above, the `PropTypes.func` part checks that `handleClick` is a function. Adding `isRequired` tells React that `handleClick` is a required property for that component. You will see a warning if that prop isn't provided. Also notice that `func` represents `function`. Among the seven JavaScript primitive types, `function` and `boolean` (written as `bool`) are the only two that use unusual spelling. In addition to the primitive types, there are other types available. For example, you can check that a prop is a React element. Please refer to the [documentation](https://reactjs.org/docs/typechecking-with-proptypes.html#proptypes) for all of the options.

**Note:** As of React `v15.5.0`, `PropTypes` is imported independently from React, like this: `import PropTypes from 'prop-types';`

Define `propTypes` for the `Items` component to require `quantity` as a prop and verify that it is of type `number`.

### Solution:
```jsx
const Items = (props) => {
	return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
};

Items.propTypes = {
	quantity: PropTypes.number.isRequired
}

Items.defaultProps = {
	quantity: 0
};
  
class ShoppingCart extends React.Component {
	constructor(props) {
		super(props);
	}
	render() {
		return <Items />
	}
};
```

## 19. Access Props Using `this.props`
The last several challenges covered the basic ways to pass props to child components. But what if the child component that you're passing a prop to is an ES6 class component, rather than a stateless functional component? The ES6 class component uses a slightly different convention to access props.

Anytime you refer to a class component within itself, you use the `this` keyword. To access props within a class component, you preface the code that you use to access it with `this`. For example, if an ES6 class component has a prop called `data`, you write `{this.props.data}` in JSX.

Render an instance of the `Welcome` component in the parent component `App`. Here, give `Welcome` a prop of `name` and assign it a value of a string. Within the child, `Welcome`, access the `name` prop within the `strong` tags.

### Solution:
```jsx
class App extends React.Component {
	constructor(props) {
		super(props);
	}
	render() {
		return (
			<div>
				{ /* Change code below this line */ }
				<Welcome name="Subahdeep"/>
				{ /* Change code above this line */ }
			</div>
		);
	}
};
  
class Welcome extends React.Component {
	constructor(props) {
		super(props);
	}
	render() {
		return (
			<div>
				{ /* Change code below this line */ }
				<p>Hello, <strong>{this.props.name}</strong>!</p>
				{ /* Change code above this line */ }
			</div>
		);
	}
};
```

## 20. Review Using Props with Stateless Functional Components
Except for the last challenge, you've been passing props to stateless functional components. These components act like pure functions. They accept props as input and return the same view every time they are passed the same props. You may be wondering what state is, and the next challenge will cover it in more detail. Before that, here's a review of the terminology for components.

A _stateless functional component_ is any function you write which accepts props and returns JSX. A _stateless component_, on the other hand, is a class that extends `React.Component`, but does not use internal state (covered in the next challenge). Finally, a _stateful component_ is a class component that does maintain its own internal state. You may see stateful components referred to simply as components or React components.

A common pattern is to try to minimize statefulness and to create stateless functional components wherever possible. This helps contain your state management to a specific area of your application. In turn, this improves development and maintenance of your app by making it easier to follow how changes to state affect its behavior.

The code editor has a `CampSite` component that renders a `Camper` component as a child. Define the `Camper` component and assign it default props of `{ name: 'CamperBot' }`. Inside the `Camper` component, render any code that you want, but make sure to have one `p` element that includes only the `name` value that is passed in as a `prop`. Finally, define `propTypes` on the `Camper` component to require `name` to be provided as a prop and verify that it is of type `string`.

### Solution:
```jsx
class CampSite extends React.Component {
	constructor(props) {
		super(props);
	}
	render() {
		return (
			<div>
				<Camper name="CamperBot"/>
			</div>
		);
	}
};

class Camper extends React.Component {
	constructor(props) {
		super(props);
	}
	  
	render() {
		return (
			<div>
				<p>{this.props.name}</p>
			</div>
		);
	}
}
  
Camper.defaultProps = {
	name: "CamperBot"
}
  
Camper.propTypes = {
	name: PropTypes.string.isRequired
}
```

## 21. Create a Stateful Component
One of the most important topics in React is `state`. State consists of any data your application needs to know about, that can change over time. You want your apps to respond to state changes and present an updated UI when necessary. React offers a nice solution for the state management of modern web applications.

You create state in a React component by declaring a `state` property on the component class in its `constructor`. This initializes the component with `state` when it is created. The `state` property must be set to a JavaScript `object`. Declaring it looks like this:

```jsx
this.state = {

}
```

You have access to the `state` object throughout the life of your component. You can update it, render it in your UI, and pass it as props to child components. The `state` object can be as complex or as simple as you need it to be. Note that you must create a class component by extending `React.Component` in order to create `state` like this.

There is a component in the code editor that is trying to render a `firstName` property from its `state`. However, there is no `state` defined. Initialize the component with `state` in the `constructor` and assign your name to a property of `firstName`.

### Solution:
```jsx
class StatefulComponent extends React.Component {
	constructor(props) {
		super(props);
		this.state = {
			firstName: "Subhadeep"
		}
	}
	render() {
		return (
			<div>
				<h1>{this.state.firstName}</h1>
			</div>
		);
	}
};
```

## 22. Render State in the User Interface
Once you define a component's initial state, you can display any part of it in the UI that is rendered. If a component is stateful, it will always have access to the data in `state` in its `render()` method. You can access the data with `this.state`.

If you want to access a state value within the `return` of the render method, you have to enclose the value in curly braces.

`state` is one of the most powerful features of components in React. It allows you to track important data in your app and render a UI in response to changes in this data. If your data changes, your UI will change. React uses what is called a virtual DOM, to keep track of changes behind the scenes. When state data updates, it triggers a re-render of the components using that data - including child components that received the data as a prop. React updates the actual DOM, but only where necessary. This means you don't have to worry about changing the DOM. You simply declare what the UI should look like.

Note that if you make a component stateful, no other components are aware of its `state`. Its `state` is completely encapsulated, or local to that component, unless you pass state data to a child component as `props`. This notion of encapsulated `state` is very important because it allows you to write certain logic, then have that logic contained and isolated in one place in your code.

In the code editor, `MyComponent` is already stateful. Define an `h1` tag in the component's render method which renders the value of `name` from the component's state.

**Note:** The `h1` should only render the value from `state` and nothing else. In JSX, any code you write with curly braces `{ }` will be treated as JavaScript. So to access the value from `state` just enclose the reference in curly braces.

### Solution:
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'freeCodeCamp'
    }
  }
  render() {
    return (
      <div>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};
```

## 23. Render State in the User Interface Another Way
There is another way to access `state` in a component. In the `render()` method, before the `return` statement, you can write JavaScript directly. For example, you could declare functions, access data from `state` or `props`, perform computations on this data, and so on. Then, you can assign any data to variables, which you have access to in the `return` statement.

In the `MyComponent` render method, define a `const` called `name` and set it equal to the name value in the component's `state`. Because you can write JavaScript directly in this part of the code, you don't have to enclose this reference in curly braces.

Next, in the return statement, render this value in an `h1` tag using the variable `name`. Remember, you need to use the JSX syntax (curly braces for JavaScript) in the return statement.

### Solution:
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'freeCodeCamp'
    }
  }
  render() {
    // Change code below this line
    const name = this.state.name
    // Change code above this line
    return (
      <div>
        { /* Change code below this line */ }
        <h1>{name}</h1>
        { /* Change code above this line */ }
      </div>
    );
  }
};
```

## 24. Set State with `this.setState`
The previous challenges covered component `state` and how to initialize state in the `constructor`. There is also a way to change the component's `state`. React provides a method for updating component `state` called `setState`. You call the `setState` method within your component class like so: `this.setState()`, passing in an object with key-value pairs. The keys are your state properties and the values are the updated state data. For instance, if we were storing a `username` in state and wanted to update it, it would look like this:

```jsx
this.setState({
  username: 'Lewis'
});
```

React expects you to never modify `state` directly, instead always use `this.setState()` when state changes occur. Also, you should note that React may batch multiple state updates in order to improve performance. What this means is that state updates through the `setState` method can be asynchronous. There is an alternative syntax for the `setState` method which provides a way around this problem. This is rarely needed but it's good to keep it in mind! Please consult our [React article](https://www.freecodecamp.org/news/what-is-state-in-react-explained-with-examples/) for further details.

There is a `button` element in the code editor which has an `onClick()` handler. This handler is triggered when the `button` receives a click event in the browser, and runs the `handleClick` method defined on `MyComponent`. Within the `handleClick` method, update the component `state` using `this.setState()`. Set the `name` property in `state` to equal the string `React Rocks!`.

Click the button and watch the rendered state update. Don't worry if you don't fully understand how the click handler code works at this point. It's covered in upcoming challenges.

### Solution:
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'Initial State'
    };
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    // Change code below this line
    this.setState({
      name: "React Rocks!"
    })
    // Change code above this line
  }
  render() {
    return (
      <div>
        <button onClick={this.handleClick}>Click Me</button>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};
```

## 25. Bind 'this' to a Class Method
In addition to setting and updating `state`, you can also define methods for your component class. A class method typically needs to use the `this` keyword so it can access properties on the class (such as `state` and `props`) inside the scope of the method. There are a few ways to allow your class methods to access `this`.

One common way is to explicitly bind `this` in the constructor so `this` becomes bound to the class methods when the component is initialized. You may have noticed the last challenge used `this.handleClick = this.handleClick.bind(this)` for its `handleClick` method in the constructor. Then, when you call a function like `this.setState()` within your class method, `this` refers to the class and will not be `undefined`.

**Note:** The `this` keyword is one of the most confusing aspects of JavaScript but it plays an important role in React. Although its behavior here is totally normal, these lessons aren't the place for an in-depth review of `this` so please refer to other lessons if the above is confusing!

The code editor has a component with a `state` that keeps track of the text. It also has a method which allows you to set the text to `You clicked!`. However, the method doesn't work because it's using the `this` keyword that is undefined. Fix it by explicitly binding `this` to the `handleClick()` method in the component's constructor.

Next, add a click handler to the `button` element in the render method. It should trigger the `handleClick()` method when the button receives a click event. Remember that the method you pass to the `onClick` handler needs curly braces because it should be interpreted directly as JavaScript.

Once you complete the above steps you should be able to click the button and see `You clicked!`.

### Solution:
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      text: "Hello"
    };
    // Change code below this line
    this.handleClick = this.handleClick.bind(this)
    // Change code above this line
  }
  handleClick() {
    this.setState({
      text: "You clicked!"
    });
  }
  render() {
    return (
      <div>
        { /* Change code below this line */ }
        <button onClick={this.handleClick}>Click Me</button>
        { /* Change code above this line */ }
        <h1>{this.state.text}</h1>
      </div>
    );
  }
};
```

## 26. Use State to Toggle an Element
Sometimes you might need to know the previous state when updating the state. However, state updates may be asynchronous - this means React may batch multiple `setState()` calls into a single update. This means you can't rely on the previous value of `this.state` or `this.props` when calculating the next value. So, you should not use code like this:

```jsx
this.setState({
  counter: this.state.counter + this.props.increment
});
```

Instead, you should pass `setState` a function that allows you to access state and props. Using a function with `setState` guarantees you are working with the most current values of state and props. This means that the above should be rewritten as:

```jsx
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

You can also use a form without `props` if you need only the `state`:

```jsx
this.setState(state => ({
  counter: state.counter + 1
}));
```

Note that you have to wrap the object literal in parentheses, otherwise JavaScript thinks it's a block of code.

`MyComponent` has a `visibility` property which is initialized to `false`. The render method returns one view if the value of `visibility` is true, and a different view if it is false.

Currently, there is no way of updating the `visibility` property in the component's `state`. The value should toggle back and forth between true and false. There is a click handler on the button which triggers a class method called `toggleVisibility()`. Pass a function to `setState` to define this method so that the `state` of `visibility` toggles to the opposite value when the method is called. If `visibility` is `false`, the method sets it to `true`, and vice versa.

Finally, click the button to see the conditional rendering of the component based on its `state`.

**Hint:** Don't forget to bind the `this` keyword to the method in the `constructor`!

### Solution:
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      visibility: false
    };
    // Change code below this line
    this.toggleVisibility = this.toggleVisibility.bind(this)
    // Change code above this line
  }
  // Change code below this line
  toggleVisibility() {
    this.setState((state) => ({
      visibility: !state.visibility
    }))
  }
  // Change code above this line
  render() {
    if (this.state.visibility) {
      return (
        <div>
          <button onClick={this.toggleVisibility}>Click Me</button>
          <h1>Now you see me!</h1>
        </div>
      );
    } else {
      return (
        <div>
          <button onClick={this.toggleVisibility}>Click Me</button>
        </div>
      );
    }
  }
}
```

## 27. Write a Simple Counter
You can design a more complex stateful component by combining the concepts covered so far. These include initializing `state`, writing methods that set `state`, and assigning click handlers to trigger these methods.

The `Counter` component keeps track of a `count` value in `state`. There are two buttons which call methods `increment()` and `decrement()`. Write these methods so the counter value is incremented or decremented by 1 when the appropriate button is clicked. Also, create a `reset()` method so when the reset button is clicked, the count is set to 0.

**Note:** Make sure you don't modify the `className`s of the buttons. Also, remember to add the necessary bindings for the newly-created methods in the constructor.

### Solution:
```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
    // Change code below this line
    this.increment = this.increment.bind(this)
    this.decrement = this.decrement.bind(this)
    this.reset = this.reset.bind(this)
    // Change code above this line
  }
  // Change code below this line
  increment() {
    this.setState((state) => ({
      count: state.count + 1
    }))
  }

  decrement() {
    this.setState((state) => ({
      count: state.count - 1
    }))
  }

  reset() {
    this.setState((state) => ({
      count: 0
    }))
  }
  // Change code above this line
  render() {
    return (
      <div>
        <button className='inc' onClick={this.increment}>Increment!</button>
        <button className='dec' onClick={this.decrement}>Decrement!</button>
        <button className='reset' onClick={this.reset}>Reset</button>
        <h1>Current Count: {this.state.count}</h1>
      </div>
    );
  }
};
```

## 28. Create a Controlled Input
Your application may have more complex interactions between `state` and the rendered UI. For example, form control elements for text input, such as `input` and `textarea`, maintain their own state in the DOM as the user types. With React, you can move this mutable state into a React component's `state`. The user's input becomes part of the application `state`, so React controls the value of that input field. Typically, if you have React components with input fields the user can type into, it will be a controlled input form.

The code editor has the skeleton of a component called `ControlledInput` to create a controlled `input` element. The component's `state` is already initialized with an `input` property that holds an empty string. This value represents the text a user types into the `input` field.

First, create a method called `handleChange()` that has a parameter called `event`. When the method is called, it receives an `event` object that contains a string of text from the `input` element. You can access this string with `event.target.value` inside the method. Update the `input` property of the component's `state` with this new string.

In the `render` method, create the `input` element above the `h4` tag. Add a `value` attribute which is equal to the `input` property of the component's `state`. Then add an `onChange()` event handler set to the `handleChange()` method.

When you type in the input box, that text is processed by the `handleChange()` method, set as the `input` property in the local `state`, and rendered as the value in the `input` box on the page. The component `state` is the single source of truth regarding the input data.

Last but not least, don't forget to add the necessary bindings in the constructor.

### Solution:
```jsx
class ControlledInput extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: ''
    };
    // Change code below this line
    this.handleChange = this.handleChange.bind(this)
    // Change code above this line
  }
  // Change code below this line
  handleChange(event) {
    this.setState({
      input: event.target.value
    })
  }
  // Change code above this line
  render() {
    return (
      <div>
        { /* Change code below this line */}
        <input value={this.state.input} onChange={this.handleChange}></input>
        { /* Change code above this line */}
        <h4>Controlled Input:</h4>
        <p>{this.state.input}</p>
      </div>
    );
  }
};
```

## 29. Create a Controlled Form
The last challenge showed that React can control the internal state for certain elements like `input` and `textarea`, which makes them controlled components. This applies to other form elements as well, including the regular HTML `form` element.

The `MyForm` component is set up with an empty `form` with a submit handler. The submit handler will be called when the form is submitted.

We've added a button which submits the form. You can see it has the `type` set to `submit` indicating it is the button controlling the form. Add the `input` element in the `form` and set its `value` and `onChange()` attributes like the last challenge. You should then complete the `handleSubmit` method so that it sets the component state property `submit` to the current input value in the local `state`.

**Note:** You also must call `event.preventDefault()` in the submit handler, to prevent the default form submit behavior which will refresh the web page. For camper convenience, the default behavior has been disabled here to prevent refreshes from resetting challenge code.

Finally, create an `h1` tag after the `form` which renders the `submit` value from the component's `state`. You can then type in the form and click the button (or press enter), and you should see your input rendered to the page.

### Solution:
```jsx
class MyForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      submit: ''
    };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  handleSubmit(event) {
    event.preventDefault();
    this.setState({
      submit: this.state.input
    })
  }
  render() {
    return (
      <div>
        <form onSubmit={this.handleSubmit}>
          <input value={this.state.input} onChange={this.handleChange}></input>
          <button type='submit'>Submit!</button>
        </form>
        <h1>{this.state.submit}</h1>
      </div>
    );
  }
}
```

## 30. Pass State as Props to Child Components
You saw a lot of examples that passed props to child JSX elements and child React components in previous challenges. You may be wondering where those props come from. A common pattern is to have a stateful component containing the `state` important to your app, that then renders child components. You want these components to have access to some pieces of that `state`, which are passed in as props.

For example, maybe you have an `App` component that renders a `Navbar`, among other components. In your `App`, you have `state` that contains a lot of user information, but the `Navbar` only needs access to the user's username so it can display it. You pass that piece of `state` to the `Navbar` component as a prop.

This pattern illustrates some important paradigms in React. The first is _unidirectional data flow_. State flows in one direction down the tree of your application's components, from the stateful parent component to child components. The child components only receive the state data they need. The second is that complex stateful apps can be broken down into just a few, or maybe a single, stateful component. The rest of your components simply receive state from the parent as props, and render a UI from that state. It begins to create a separation where state management is handled in one part of code and UI rendering in another. This principle of separating state logic from UI logic is one of React's key principles. When it's used correctly, it makes the design of complex, stateful applications much easier to manage.

The `MyApp` component is stateful and renders a `Navbar` component as a child. Pass the `name` property in its `state` down to the child component, then show the `name` in the `h1` tag that's part of the `Navbar` render method. `name` should appear after the text `Hello, my name is:`.

### Solution:
```jsx
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'CamperBot'
    }
  }
  render() {
    return (
       <div>
         <Navbar name={this.state.name}/>
       </div>
    );
  }
};

class Navbar extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
    <div>
      <h1>Hello, my name is: {this.props.name}</h1>
    </div>
    );
  }
};
```

## 31. Pass a Callback as Props
You can pass `state` as props to child components, but you're not limited to passing data. You can also pass handler functions or any method that's defined on a React component to a child component. This is how you allow child components to interact with their parent components. You pass methods to a child just like a regular prop. It's assigned a name and you have access to that method name under `this.props` in the child component.

There are three components outlined in the code editor. The `MyApp` component is the parent that will render the `GetInput` and `RenderInput` child components. Add the `GetInput` component to the render method in `MyApp`, then pass it a prop called `input` assigned to `inputValue` from `MyApp`'s `state`. Also create a prop called `handleChange` and pass the input handler `handleChange` to it.

Next, add `RenderInput` to the render method in `MyApp`, then create a prop called `input` and pass the `inputValue` from `state` to it. Once you are finished you will be able to type in the `input` field in the `GetInput` component, which then calls the handler method in its parent via props. This updates the input in the `state` of the parent, which is passed as props to both children. Observe how the data flows between the components and how the single source of truth remains the `state` of the parent component. Admittedly, this example is a bit contrived, but should serve to illustrate how data and callbacks can be passed between React components.

### Solution:
```jsx
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      inputValue: ''
    }
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({
      inputValue: event.target.value
    });
  }
  render() {
    return (
       <div>
        <GetInput input={this.state.inputValue} handleChange={this.handleChange}/>
        <RenderInput input={this.state.inputValue} />
       </div>
    );
  }
};

class GetInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Get Input:</h3>
        <input
          value={this.props.input}
          onChange={this.props.handleChange}/>
      </div>
    );
  }
};

class RenderInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Input Render:</h3>
        <p>{this.props.input}</p>
      </div>
    );
  }
};
```

## 32. Use the Lifecycle Method `componentWillMount`
React components have several special methods that provide opportunities to perform actions at specific points in the lifecycle of a component. These are called lifecycle methods, or lifecycle hooks, and allow you to catch components at certain points in time. This can be before they are rendered, before they update, before they receive props, before they unmount, and so on. Here is a list of some of the main lifecycle methods: `componentWillMount()` `componentDidMount()` `shouldComponentUpdate()` `componentDidUpdate()` `componentWillUnmount()` The next several lessons will cover some of the basic use cases for these lifecycle methods.

**Note:** The `componentWillMount` Lifecycle method will be deprecated in a future version of 16.X and removed in version 17. Learn more in this [article](https://www.freecodecamp.org/news/how-to-safely-use-reacts-life-cycles-with-fiber-s-async-rendering-fd4469ebbd8f/)

The `componentWillMount()` method is called before the `render()` method when a component is being mounted to the DOM. Log something to the console within `componentWillMount()` - you may want to have your browser console open to see the output.

### Solution:
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  componentWillMount() {
    console.log("componentWillMount")
  }
  render() {
    return <div />
  }
};
```

## 33. Use the Lifecycle Method `componentDidMount`
Most web developers, at some point, need to call an API endpoint to retrieve data. If you're working with React, it's important to know where to perform this action.

The best practice with React is to place API calls or any calls to your server in the lifecycle method `componentDidMount()`. This method is called after a component is mounted to the DOM. Any calls to `setState()` here will trigger a re-rendering of your component. When you call an API in this method, and set your state with the data that the API returns, it will automatically trigger an update once you receive the data.

There is a mock API call in `componentDidMount()`. It sets state after 2.5 seconds to simulate calling a server to retrieve data. This example requests the current total active users for a site. In the render method, render the value of `activeUsers` in the `h1` after the text `Active Users:`. Watch what happens in the preview, and feel free to change the timeout to see the different effects.

### Solution:
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      activeUsers: null
    };
  }
  componentDidMount() {
    setTimeout(() => {
      this.setState({
        activeUsers: 1273
      });
    }, 2500);
  }
  render() {
    return (
      <div>
        <h1>Active Users: {this.state.activeUsers}</h1>
      </div>
    );
  }
}
```

## 34. Add Event Listeners
The `componentDidMount()` method is also the best place to attach any event listeners you need to add for specific functionality. React provides a synthetic event system which wraps the native event system present in browsers. This means that the synthetic event system behaves exactly the same regardless of the user's browser - even if the native events may behave differently between different browsers.

You've already been using some of these synthetic event handlers such as `onClick()`. React's synthetic event system is great to use for most interactions you'll manage on DOM elements. However, if you want to attach an event handler to the document or window objects, you have to do this directly.

Attach an event listener in the `componentDidMount()` method for `keydown` events and have these events trigger the callback `handleKeyPress()`. You can use `document.addEventListener()` which takes the event (in quotes) as the first argument and the callback as the second argument.

Then, in `componentWillUnmount()`, remove this same event listener. You can pass the same arguments to `document.removeEventListener()`. It's good practice to use this lifecycle method to do any clean up on React components before they are unmounted and destroyed. Removing event listeners is an example of one such clean up action.

### Solution:
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      message: ''
    };
    this.handleEnter = this.handleEnter.bind(this);
    this.handleKeyPress = this.handleKeyPress.bind(this);
  }
  componentDidMount() {
    document.addEventListener("keydown", this.handleKeyPress)
  }
  componentWillUnmount() {
    document.removeEventListener("keydown", this.handleKeyPress)
  }
  handleEnter() {
    this.setState((state) => ({
      message: state.message + 'You pressed the enter key! '
    }));
  }
  handleKeyPress(event) {
    if (event.keyCode === 13) {
      this.handleEnter();
    }
  }
  render() {
    return (
      <div>
        <h1>{this.state.message}</h1>
      </div>
    );
  }
};
```

## 35. Optimize Re-Renders with `shouldComponentUpdate`
So far, if any component receives new `state` or new `props`, it re-renders itself and all its children. This is usually okay. But React provides a lifecycle method you can call when child components receive new `state` or `props`, and declare specifically if the components should update or not. The method is `shouldComponentUpdate()`, and it takes `nextProps` and `nextState` as parameters.

This method is a useful way to optimize performance. For example, the default behavior is that your component re-renders when it receives new `props`, even if the `props` haven't changed. You can use `shouldComponentUpdate()` to prevent this by comparing the `props`. The method must return a `boolean` value that tells React whether or not to update the component. You can compare the current props (`this.props`) to the next props (`nextProps`) to determine if you need to update or not, and return `true` or `false` accordingly.

The `shouldComponentUpdate()` method is added in a component called `OnlyEvens`. Currently, this method returns `true` so `OnlyEvens` re-renders every time it receives new `props`. Modify the method so `OnlyEvens` updates only if the `value` of its new props is even. Click the `Add` button and watch the order of events in your browser's console as the lifecycle hooks are triggered.

### Solution:
```jsx
class OnlyEvens extends React.Component {
  constructor(props) {
    super(props);
  }
  shouldComponentUpdate(nextProps, nextState) {
    console.log('Should I update?');
    if (nextProps.value % 2 === 0)
      return true;
    else 
      return false;
  }
  componentDidUpdate() {
    console.log('Component re-rendered.');
  }
  render() {
    return <h1>{this.props.value}</h1>;
  }
}

class Controller extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 0
    };
    this.addValue = this.addValue.bind(this);
  }
  addValue() {
    this.setState(state => ({
      value: state.value + 1
    }));
  }
  render() {
    return (
      <div>
        <button onClick={this.addValue}>Add</button>
        <OnlyEvens value={this.state.value} />
      </div>
    );
  }
}
```

## 36. Introducing Inline Styles
There are other complex concepts that add powerful capabilities to your React code. But you may be wondering about the more simple problem of how to style those JSX elements you create in React. You likely know that it won't be exactly the same as working with HTML because of [the way you apply classes to JSX elements](https://www.freecodecamp.org/learn/front-end-development-libraries/react/define-an-html-class-in-jsx).

If you import styles from a stylesheet, it isn't much different at all. You apply a class to your JSX element using the `className` attribute, and apply styles to the class in your stylesheet. Another option is to apply inline styles, which are very common in ReactJS development.

You apply inline styles to JSX elements similar to how you do it in HTML, but with a few JSX differences. Here's an example of an inline style in HTML:

```jsx
<div style="color: yellow; font-size: 16px">Mellow Yellow</div>
```

JSX elements use the `style` attribute, but because of the way JSX is transpiled, you can't set the value to a `string`. Instead, you set it equal to a JavaScript `object`. Here's an example:

```jsx
<div style={{color: "yellow", fontSize: 16}}>Mellow Yellow</div>
```

Notice how we camel-Case the `fontSize` property? This is because React will not accept kebab-case keys in the style object. React will apply the correct property name for us in the HTML.

Add a `style` attribute to the `div` in the code editor to give the text a color of red and font size of `72px`.

Note that you can optionally set the font size to be a number, omitting the units `px`, or write it as `72px`.

### Solution:
```jsx
class Colorful extends React.Component {
  render() {
    return (
      <div style={{color: "red", fontSize: 72 }}>Big Red</div>
    );
  }
};
```

## 37. Add Inline Styles in React
You may have noticed in the last challenge that there were several other syntax differences from HTML inline styles in addition to the `style` attribute set to a JavaScript object. First, the names of certain CSS style properties use camel case. For example, the last challenge set the size of the font with `fontSize` instead of `font-size`. Hyphenated words like `font-size` are invalid syntax for JavaScript object properties, so React uses camel case. As a rule, any hyphenated style properties are written using camel case in JSX.

All property value length units (like `height`, `width`, and `fontSize`) are assumed to be in `px` unless otherwise specified. If you want to use `em`, for example, you wrap the value and the units in quotes, like `{fontSize: "4em"}`. Other than the length values that default to `px`, all other property values should be wrapped in quotes.

If you have a large set of styles, you can assign a style `object` to a constant to keep your code organized. Declare your styles constant as a global variable at the top of the file. Initialize `styles` constant and assign an `object` with three style properties and their values to it. Give the `div` a color of `purple`, a font-size of `40`, and a border of `2px solid purple`. Then set the `style` attribute equal to the `styles` constant.

### Solution:
```jsx
const styles = {
  color: "purple",
  fontSize: 40,
  border: "2px solid purple",
}

class Colorful extends React.Component {
  render() {
    return (
      <div style={styles}>Style Me!</div>
    );
  }
};
```

## 38. Use Advanced JavaScript in React Render Method
In previous challenges, you learned how to inject JavaScript code into JSX code using curly braces, `{ }`, for tasks like accessing props, passing props, accessing state, inserting comments into your code, and most recently, styling your components. These are all common use cases to put JavaScript in JSX, but they aren't the only way that you can utilize JavaScript code in your React components.

You can also write JavaScript directly in your `render` methods, before the `return` statement, _**without**_ inserting it inside of curly braces. This is because it is not yet within the JSX code. When you want to use a variable later in the JSX code _inside_ the `return` statement, you place the variable name inside curly braces.

In the code provided, the `render` method has an array that contains 20 phrases to represent the answers found in the classic 1980's Magic Eight Ball toy. The button click event is bound to the `ask` method, so each time the button is clicked a random number will be generated and stored as the `randomIndex` in state. On line 52, delete the string `change me!` and reassign the `answer` const so your code randomly accesses a different index of the `possibleAnswers` array each time the component updates. Finally, insert the `answer` const inside the `p` tags.

### Solution:
```jsx
const inputStyle = {
  width: 235,
  margin: 5
};

class MagicEightBall extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      userInput: '',
      randomIndex: ''
    };
    this.ask = this.ask.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  ask() {
    if (this.state.userInput) {
      this.setState({
        randomIndex: Math.floor(Math.random() * 20),
        userInput: ''
      });
    }
  }
  handleChange(event) {
    this.setState({
      userInput: event.target.value
    });
  }
  render() {
    const possibleAnswers = [
      'It is certain',
      'It is decidedly so',
      'Without a doubt',
      'Yes, definitely',
      'You may rely on it',
      'As I see it, yes',
      'Outlook good',
      'Yes',
      'Signs point to yes',
      'Reply hazy try again',
      'Ask again later',
      'Better not tell you now',
      'Cannot predict now',
      'Concentrate and ask again',
      "Don't count on it",
      'My reply is no',
      'My sources say no',
      'Most likely',
      'Outlook not so good',
      'Very doubtful'
    ];
    const answer = possibleAnswers[this.state.randomIndex]; // Change this line
    return (
      <div>
        <input
          type='text'
          value={this.state.userInput}
          onChange={this.handleChange}
          style={inputStyle}
        />
        <br />
        <button onClick={this.ask}>Ask the Magic Eight Ball!</button>
        <br />
        <h3>Answer:</h3>
        <p>
          {answer}
        </p>
      </div>
    );
  }
}
```

## 39. Render with an If-Else Condition
Another application of using JavaScript to control your rendered view is to tie the elements that are rendered to a condition. When the condition is true, one view renders. When it's false, it's a different view. You can do this with a standard `if/else` statement in the `render()` method of a React component.

`MyComponent` contains a `boolean` in its state which tracks whether you want to display some element in the UI or not. The `button` toggles the state of this value. Currently, it renders the same UI every time. Rewrite the `render()` method with an `if/else` statement so that if `display` is `true`, you return the current markup. Otherwise, return the markup without the `h1` element.

**Note:** You must write an `if/else` to pass the tests. Use of the ternary operator will not pass here.

### Solution:
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      display: true
    }
    this.toggleDisplay = this.toggleDisplay.bind(this);
  }
  toggleDisplay() {
    this.setState((state) => ({
      display: !state.display
    }));
  }
  render() {
    if (this.state.display)
    return (
       <div>
         <button onClick={this.toggleDisplay}>Toggle Display</button>
         <h1>Displayed!</h1>
       </div>
    );
    else
    return (
      <div>
         <button onClick={this.toggleDisplay}>Toggle Display</button>
       </div>
    )
  }
};
```

## 40. Use && for a More Concise Conditional
The `if/else` statements worked in the last challenge, but there's a more concise way to achieve the same result. Imagine that you are tracking several conditions in a component and you want different elements to render depending on each of these conditions. If you write a lot of `else if` statements to return slightly different UIs, you may repeat code which leaves room for error. Instead, you can use the `&&` logical operator to perform conditional logic in a more concise way. This is possible because you want to check if a condition is `true`, and if it is, return some markup. Here's an example:

```jsx
{condition && <p>markup</p>}
```

If the `condition` is `true`, the markup will be returned. If the condition is `false`, the operation will immediately return `false` after evaluating the `condition` and return nothing. You can include these statements directly in your JSX and string multiple conditions together by writing `&&` after each one. This allows you to handle more complex conditional logic in your `render()` method without repeating a lot of code.

Solve the previous example again, so the `h1` only renders if `display` is `true`, but use the `&&` logical operator instead of an `if/else` statement.

### Solution:
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      display: true
    }
    this.toggleDisplay = this.toggleDisplay.bind(this);
  }
  toggleDisplay() {
    this.setState(state => ({
      display: !state.display
    }));
  }
  render() {
    return (
       <div>
         <button onClick={this.toggleDisplay}>Toggle Display</button>
         {this.state.display && <h1>Displayed!</h1>}
       </div>
    );

  }
};
```

## 41. Use a Ternary Expression for Conditional Rendering
Before moving on to dynamic rendering techniques, there's one last way to use built-in JavaScript conditionals to render what you want: the ternary operator. The ternary operator is often utilized as a shortcut for `if/else` statements in JavaScript. They're not quite as robust as traditional `if/else` statements, but they are very popular among React developers. One reason for this is because of how JSX is compiled, `if/else` statements can't be inserted directly into JSX code. You might have noticed this a couple challenges ago — when an `if/else` statement was required, it was always _outside_ the `return` statement. Ternary expressions can be an excellent alternative if you want to implement conditional logic within your JSX. Recall that a ternary operator has three parts, but you can combine several ternary expressions together. Here's the basic syntax:

```jsx
condition ? expressionIfTrue : expressionIfFalse;
```

The code editor has three constants defined within the `CheckUserAge` component's `render()` method. They are called `buttonOne`, `buttonTwo`, and `buttonThree`. Each of these is assigned a simple JSX expression representing a button element. First, initialize the state of `CheckUserAge` with `input` and `userAge` both set to values of an empty string.

Once the component is rendering information to the page, users should have a way to interact with it. Within the component's `return` statement, set up a ternary expression that implements the following logic: when the page first loads, render the submit button, `buttonOne`, to the page. Then, when a user enters their age and clicks the button, render a different button based on the age. If a user enters a number less than `18`, render `buttonThree`. If a user enters a number greater than or equal to `18`, render `buttonTwo`.

### Solution:
```jsx
const inputStyle = {
  width: 235,
  margin: 5
};

class CheckUserAge extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: "",
      userAge: ""
    }
    this.submit = this.submit.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(e) {
    this.setState({
      input: e.target.value,
      userAge: ''
    });
  }
  submit() {
    this.setState(state => ({
      userAge: state.input
    }));
  }
  render() {
    const buttonOne = <button onClick={this.submit}>Submit</button>;
    const buttonTwo = <button>You May Enter</button>;
    const buttonThree = <button>You Shall Not Pass</button>;
    return (
      <div>
        <h3>Enter Your Age to Continue</h3>
        <input
          style={inputStyle}
          type='number'
          value={this.state.input}
          onChange={this.handleChange}
        />
        <br />
        {this.state.userAge === "" ? buttonOne
        : this.state.userAge >= 18 ?
          buttonTwo : buttonThree
        }
      </div>
    );
  }
}
```

## 42. Render Conditionally from Props
So far, you've seen how to use `if/else`, `&&`, and the ternary operator (`condition ? expressionIfTrue : expressionIfFalse`) to make conditional decisions about what to render and when. However, there's one important topic left to discuss that lets you combine any or all of these concepts with another powerful React feature: props. Using props to conditionally render code is very common with React developers — that is, they use the value of a given prop to automatically make decisions about what to render.

In this challenge, you'll set up a child component to make rendering decisions based on props. You'll also use the ternary operator, but you can see how several of the other concepts that were covered in the last few challenges might be just as useful in this context.

The code editor has two components that are partially defined for you: a parent called `GameOfChance`, and a child called `Results`. They are used to create a simple game where the user presses a button to see if they win or lose.

First, you'll need a simple expression that randomly returns a different value every time it is run. You can use `Math.random()`. This method returns a value between `0` (inclusive) and `1` (exclusive) each time it is called. So for 50/50 odds, use `Math.random() >= .5` in your expression. Statistically speaking, this expression will return `true` 50% of the time, and `false` the other 50%. In the render method, replace `null` with the above expression to complete the variable declaration.

Now you have an expression that you can use to make a randomized decision in the code. Next you need to implement this. Render the `Results` component as a child of `GameOfChance`, and pass in `expression` as a prop called `fiftyFifty`. In the `Results` component, write a ternary expression to render the `h1` element with the text `You Win!` or `You Lose!` based on the `fiftyFifty` prop that's being passed in from `GameOfChance`. Finally, make sure the `handleClick()` method is correctly counting each turn so the user knows how many times they've played. This also serves to let the user know the component has actually updated in case they win or lose twice in a row.

### Solution:
```jsx
class Results extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (<div>
      {this.props.fiftyFifty ? <h1>You Win!</h1> : <h1>You Lose!</h1>}
    </div>)
  }
}

class GameOfChance extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 1
    };
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    this.setState(prevState => {
      return {
        counter: prevState.counter + 1,
      }
    });
  }
  render() {
    const expression = Math.random(0, 1) >= 0.5;
    return (
      <div>
        <button onClick={this.handleClick}>Play Again</button>
        <Results fiftyFifty={expression}/>
        <p>{'Turn: ' + this.state.counter}</p>
      </div>
    );
  }
}
```

## 43. Change Inline CSS Conditionally Based on Component State
At this point, you've seen several applications of conditional rendering and the use of inline styles. Here's one more example that combines both of these topics. You can also render CSS conditionally based on the state of a React component. To do this, you check for a condition, and if that condition is met, you modify the styles object that's assigned to the JSX elements in the render method.

This paradigm is important to understand because it is a dramatic shift from the more traditional approach of applying styles by modifying DOM elements directly (which is very common with jQuery, for example). In that approach, you must keep track of when elements change and also handle the actual manipulation directly. It can become difficult to keep track of changes, potentially making your UI unpredictable. When you set a style object based on a condition, you describe how the UI should look as a function of the application's state. There is a clear flow of information that only moves in one direction. This is the preferred method when writing applications with React.

The code editor has a simple controlled input component with a styled border. You want to style this border red if the user types more than 15 characters of text in the input box. Add a condition to check for this and, if the condition is valid, set the input border style to `3px solid red`. You can try it out by entering text in the input.

### Solution:
```jsx
class GateKeeper extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: ''
    };
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({ input: event.target.value })
  }
  render() {
    let inputStyle = {
      border: '1px solid black'
    };

    if (this.state.input.length > 15)
      inputStyle.border = "3px solid red"
    return (
      <div>
        <h3>Don't Type Too Much:</h3>
        <input
          type="text"
          style={inputStyle}
          value={this.state.input}
          onChange={this.handleChange} />
      </div>
    );
  }
};
```

## 44. Use `Array.map()` to Dynamically Render Elements
Conditional rendering is useful, but you may need your components to render an unknown number of elements. Often in reactive programming, a programmer has no way to know what the state of an application is until runtime, because so much depends on a user's interaction with that program. Programmers need to write their code to correctly handle that unknown state ahead of time. Using `Array.map()` in React illustrates this concept.

For example, you create a simple "To Do List" app. As the programmer, you have no way of knowing how many items a user might have on their list. You need to set up your component to dynamically render the correct number of list elements long before someone using the program decides that today is laundry day.

The code editor has most of the `MyToDoList` component set up. Some of this code should look familiar if you completed the controlled form challenge. You'll notice a `textarea` and a `button`, along with a couple of methods that track their states, but nothing is rendered to the page yet.

Inside the `constructor`, create a `this.state` object and define two states: `userInput` should be initialized as an empty string, and `toDoList` should be initialized as an empty array. Next, delete the `null` value in the `render()` method next to the `items` variable. In its place, map over the `toDoList` array stored in the component's internal state and dynamically render a `li` for each item. Try entering the string `eat, code, sleep, repeat` into the `textarea`, then click the button and see what happens.

**Note:** You may know that all sibling child elements created by a mapping operation like this do need to be supplied with a unique `key` attribute. Don't worry, this is the topic of the next challenge.

### Solution:
```jsx
const textAreaStyles = {
  width: 235,
  margin: 5
};

class MyToDoList extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      userInput: "",
      toDoList: [],
    }
    this.handleSubmit = this.handleSubmit.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  handleSubmit() {
    const itemsArray = this.state.userInput.split(',');
    this.setState({
      toDoList: itemsArray
    });
  }
  handleChange(e) {
    this.setState({
      userInput: e.target.value
    });
  }
  render() {
    const items = this.state.toDoList.map((item) => {
      return (<li>{item}</li>)
    });
    
    return (
      <div>
        <textarea
          onChange={this.handleChange}
          value={this.state.userInput}
          style={textAreaStyles}
          placeholder='Separate Items With Commas'
        />
        <br />
        <button onClick={this.handleSubmit}>Create List</button>
        <h1>My "To Do" List:</h1>
        <ul>{items}</ul>
      </div>
    );
  }
}
```

## 45. Give Sibling Elements a Unique Key Attribute
The last challenge showed how the `map` method is used to dynamically render a number of elements based on user input. However, there was an important piece missing from that example. When you create an array of elements, each one needs a `key` attribute set to a unique value. React uses these keys to keep track of which items are added, changed, or removed. This helps make the re-rendering process more efficient when the list is modified in any way.

**Note:** Keys only need to be unique between sibling elements, they don't need to be globally unique in your application.

The code editor has an array with some front end frameworks and a stateless functional component named `Frameworks()`. `Frameworks()` needs to map the array to an unordered list, much like in the last challenge. Finish writing the `map` callback to return an `li` element for each framework in the `frontEndFrameworks` array. This time, make sure to give each `li` a `key` attribute, set to a unique value. The `li` elements should also contain text from `frontEndFrameworks`.

Normally, you want to make the key something that uniquely identifies the element being rendered. As a last resort the array index may be used, but typically you should try to use a unique identification.

### Solution:
```jsx
const frontEndFrameworks = [
  'React',
  'Angular',
  'Ember',
  'Knockout',
  'Backbone',
  'Vue'
];

function Frameworks() {
  const renderFrameworks = frontEndFrameworks.map((item, index) => {
    return (<li key={index}>{item}</li>)
  }); // Change this line
  return (
    <div>
      <h1>Popular Front End JavaScript Frameworks</h1>
      <ul>
        {renderFrameworks}
      </ul>
    </div>
  );
};
```

## 46. Use `Array.filter()` to Dynamically Filter an Array
The `map` array method is a powerful tool that you will use often when working with React. Another method related to `map` is `filter`, which filters the contents of an array based on a condition, then returns a new array. For example, if you have an array of users that all have a property `online` which can be set to `true` or `false`, you can filter only those users that are online by writing:

```js
let onlineUsers = users.filter(user => user.online);
```

In the code editor, `MyComponent`'s `state` is initialized with an array of users. Some users are online and some aren't. Filter the array so you see only the users who are online. To do this, first use `filter` to return a new array containing only the users whose `online` property is `true`. Then, in the `renderOnline` variable, map over the filtered array, and return a `li` element for each user that contains the text of their `username`. Be sure to include a unique `key` as well, like in the last challenges.

### Solution:
```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      users: [
        {
          username: 'Jeff',
          online: true
        },
        {
          username: 'Alan',
          online: false
        },
        {
          username: 'Mary',
          online: true
        },
        {
          username: 'Jim',
          online: false
        },
        {
          username: 'Sara',
          online: true
        },
        {
          username: 'Laura',
          online: true
        }
      ]
    };
  }
  render() {
    const usersOnline = this.state.users.filter((user) => user.online);
    const renderOnline = usersOnline.map((user,index) => {
      return (<li key={index}>{user.username}</li>)
    });
    return (
      <div>
        <h1>Current Online Users:</h1>
        <ul>{renderOnline}</ul>
      </div>
    );
  }
}
```

## 47. Render React on the Server with `renderToString`
So far, you have been rendering React components on the client. Normally, this is what you will always do. However, there are some use cases where it makes sense to render a React component on the server. Since React is a JavaScript view library and you can run JavaScript on the server with Node, this is possible. In fact, React provides a `renderToString()` method you can use for this purpose.

There are two key reasons why rendering on the server may be used in a real world app. First, without doing this, your React apps would consist of a relatively empty HTML file and a large bundle of JavaScript when it's initially loaded to the browser. This may not be ideal for search engines that are trying to index the content of your pages so people can find you. If you render the initial HTML markup on the server and send this to the client, the initial page load contains all of the page's markup which can be crawled by search engines. Second, this creates a faster initial page load experience because the rendered HTML is smaller than the JavaScript code of the entire app. React will still be able to recognize your app and manage it after the initial load.

The `renderToString()` method is provided on `ReactDOMServer`, which is available here as a global object. The method takes one argument which is a React element. Use this to render `App` to a string.

### Solution:
```jsx
class App extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <div/>
  }
};

ReactDOMServer.renderToString(<App/>)
```


# Redux

## 1. Create a Redux Store
Redux is a state management framework that can be used with a number of different web technologies, including React.

In Redux, there is a single state object that's responsible for the entire state of your application. This means if you had a React app with ten components, and each component had its own local state, the entire state of your app would be defined by a single state object housed in the Redux `store`. This is the first important principle to understand when learning Redux: the Redux store is the single source of truth when it comes to application state.

This also means that any time any piece of your app wants to update state, it **must** do so through the Redux store. The unidirectional data flow makes it easier to track state management in your app.

The Redux `store` is an object which holds and manages application `state`. There is a method called `createStore()` on the Redux object, which you use to create the Redux `store`. This method takes a `reducer` function as a required argument. The `reducer` function is covered in a later challenge, and is already defined for you in the code editor. It simply takes `state` as an argument and returns `state`.

Declare a `store` variable and assign it to the `createStore()` method, passing in the `reducer` as an argument.

**Note:** The code in the editor uses ES6 default argument syntax to initialize this state to hold a value of `5`. If you're not familiar with default arguments, you can refer to the [ES6 section in the Curriculum](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/es6/set-default-parameters-for-your-functions) which covers this topic.

### Solution:
```jsx
const reducer = (state = 5) => {
  return state;
}

const store = Redux.createStore(reducer)
```

## 2. Get State from the Redux Store
The Redux store object provides several methods that allow you to interact with it. For example, you can retrieve the current `state` held in the Redux store object with the `getState()` method.

The code from the previous challenge is re-written more concisely in the code editor. Use `store.getState()` to retrieve the `state` from the `store`, and assign this to a new variable `currentState`.

### Solution:
```jsx
const store = Redux.createStore(
  (state = 5) => state
);

const currentState = store.getState()
```

## 3. Define a Redux Action
Since Redux is a state management framework, updating state is one of its core tasks. In Redux, all state updates are triggered by dispatching actions. An action is simply a JavaScript object that contains information about an action event that has occurred. The Redux store receives these action objects, then updates its state accordingly. Sometimes a Redux action also carries some data. For example, the action carries a username after a user logs in. While the data is optional, actions must carry a `type` property that specifies the 'type' of action that occurred.

Think of Redux actions as messengers that deliver information about events happening in your app to the Redux store. The store then conducts the business of updating state based on the action that occurred.

Writing a Redux action is as simple as declaring an object with a type property. Declare an object `action` and give it a property `type` set to the string `'LOGIN'`.

### Solution:
```jsx
const action = {
	type: 'LOGIN'
}
```

## 4. Define an Action Creator
After creating an action, the next step is sending the action to the Redux store so it can update its state. In Redux, you define action creators to accomplish this. An action creator is simply a JavaScript function that returns an action. In other words, action creators create objects that represent action events.

Define a function named `actionCreator()` that returns the `action` object when called.

### Solution:
```jsx
const action = {
	type: 'LOGIN'
}

function actionCreator() {
	return action
}
```

## 5. Dispatch an Action Event
`dispatch` method is what you use to dispatch actions to the Redux store. Calling `store.dispatch()` and passing the value returned from an action creator sends an action back to the store.

Recall that action creators return an object with a type property that specifies the action that has occurred. Then the method dispatches an action object to the Redux store. Based on the previous challenge's example, the following lines are equivalent, and both dispatch the action of type `LOGIN`:

```js
store.dispatch(actionCreator());
store.dispatch({ type: 'LOGIN' });
```

The Redux store in the code editor has an initialized state that's an object containing a `login` property currently set to `false`. There's also an action creator called `loginAction()` which returns an action of type `LOGIN`. Dispatch the `LOGIN` action to the Redux store by calling the `dispatch` method, and pass in the action created by `loginAction()`.

### Solution:
```jsx
const store = Redux.createStore(
  (state = {login: false}) => state
);

const loginAction = () => {
  return {
    type: 'LOGIN'
  }
};

store.dispatch(loginAction())
```

## 6. Handle an Action in the Store
After an action is created and dispatched, the Redux store needs to know how to respond to that action. This is the job of a `reducer` function. Reducers in Redux are responsible for the state modifications that take place in response to actions. A `reducer` takes `state` and `action` as arguments, and it always returns a new `state`. It is important to see that this is the **only** role of the reducer. It has no side effects — it never calls an API endpoint and it never has any hidden surprises. The reducer is simply a pure function that takes state and action, then returns new state.

Another key principle in Redux is that `state` is read-only. In other words, the `reducer` function must **always** return a new copy of `state` and never modify state directly. Redux does not enforce state immutability, however, you are responsible for enforcing it in the code of your reducer functions. You'll practice this in later challenges.

The code editor has the previous example as well as the start of a `reducer` function for you. Fill in the body of the `reducer` function so that if it receives an action of type `'LOGIN'` it returns a state object with `login` set to `true`. Otherwise, it returns the current `state`. Note that the current `state` and the dispatched `action` are passed to the reducer, so you can access the action's type directly with `action.type`.

### Solution:
```jsx
const defaultState = {
  login: false
};

const reducer = (state = defaultState, action) => {
  if (action.type === "LOGIN"){
    return {
      login: true
    }
  }
  else
    return state
};

const store = Redux.createStore(reducer);

const loginAction = () => {
  return {
    type: 'LOGIN'
  }
};
```

## 7. Use a Switch Statement to Handle Multiple Actions
You can tell the Redux store how to handle multiple action types. Say you are managing user authentication in your Redux store. You want to have a state representation for when users are logged in and when they are logged out. You represent this with a single state object with the property `authenticated`. You also need action creators that create actions corresponding to user login and user logout, along with the action objects themselves.

The code editor has a store, actions, and action creators set up for you. Fill in the `reducer` function to handle multiple authentication actions. Use a JavaScript `switch` statement in the `reducer` to respond to different action events. This is a standard pattern in writing Redux reducers. The switch statement should switch over `action.type` and return the appropriate authentication state.

**Note:** At this point, don't worry about state immutability, since it is small and simple in this example. For each action, you can return a new object — for example, `{authenticated: true}`. Also, don't forget to write a `default` case in your switch statement that returns the current `state`. This is important because once your app has multiple reducers, they are all run any time an action dispatch is made, even when the action isn't related to that reducer. In such a case, you want to make sure that you return the current `state`.

### Solution:
```jsx
const defaultState = {
  authenticated: false
};

const authReducer = (state = defaultState, action) => {
  switch(action.type) {
    case "LOGIN":
      return {
        authenticated: true
      }

    case "LOGOUT":
      return {
        authenticated: false
      }
    default:
      return state
  }
};

const store = Redux.createStore(authReducer);

const loginUser = () => {
  return {
    type: 'LOGIN'
  }
};

const logoutUser = () => {
  return {
    type: 'LOGOUT'
  }
};
```

## 8. Use const for Action Types
A common practice when working with Redux is to assign action types as read-only constants, then reference these constants wherever they are used. You can refactor the code you're working with to write the action types as `const` declarations.

Declare `LOGIN` and `LOGOUT` as `const` values and assign them to the strings `'LOGIN'` and `'LOGOUT'`, respectively. Then, edit the `authReducer()` and the action creators to reference these constants instead of string values.

**Note:** It's generally a convention to write constants in all uppercase, and this is standard practice in Redux as well.

### Solution:
```jsx
const LOGIN = "LOGIN"
const LOGOUT = "LOGOUT"

const defaultState = {
  authenticated: false
};

const authReducer = (state = defaultState, action) => {

  switch (action.type) {
    case LOGIN: 
      return {
        authenticated: true
      }
    case LOGOUT: 
      return {
        authenticated: false
      }
    default:
      return state;
  }

};

const store = Redux.createStore(authReducer);

const loginUser = () => {
  return {
    type: LOGIN
  }
};

const logoutUser = () => {
  return {
    type: LOGOUT
  }
};
```

## 9. Register a Store Listener
Another method you have access to on the Redux `store` object is `store.subscribe()`. This allows you to subscribe listener functions to the store, which are called whenever an action is dispatched against the store. One simple use for this method is to subscribe a function to your store that simply logs a message every time an action is received and the store is updated.

Write a callback function that increments the global variable `count` every time the store receives an action, and pass this function in to the `store.subscribe()` method. You'll see that `store.dispatch()` is called three times in a row, each time directly passing in an action object. Watch the console output between the action dispatches to see the updates take place.

### Solution:
```jsx
const ADD = 'ADD';

const reducer = (state = 0, action) => {
  switch(action.type) {
    case ADD:
      return state + 1;
    default:
      return state;
  }
};

const store = Redux.createStore(reducer);

let count = 0;

store.subscribe(() => {
  count++;
})

store.dispatch({type: ADD});
console.log(count);
store.dispatch({type: ADD});
console.log(count);
store.dispatch({type: ADD});
console.log(count);
```

## 10.  Combine Multiple Reducers
When the state of your app begins to grow more complex, it may be tempting to divide state into multiple pieces. Instead, remember the first principle of Redux: all app state is held in a single state object in the store. Therefore, Redux provides reducer composition as a solution for a complex state model. You define multiple reducers to handle different pieces of your application's state, then compose these reducers together into one root reducer. The root reducer is then passed into the Redux `createStore()` method.

In order to let us combine multiple reducers together, Redux provides the `combineReducers()` method. This method accepts an object as an argument in which you define properties which associate keys to specific reducer functions. The name you give to the keys will be used by Redux as the name for the associated piece of state.

Typically, it is a good practice to create a reducer for each piece of application state when they are distinct or unique in some way. For example, in a note-taking app with user authentication, one reducer could handle authentication while another handles the text and notes that the user is submitting. For such an application, we might write the `combineReducers()` method like this:

```js
const rootReducer = Redux.combineReducers({
  auth: authenticationReducer,
  notes: notesReducer
});
```

Now, the key `notes` will contain all of the state associated with our notes and handled by our `notesReducer`. This is how multiple reducers can be composed to manage more complex application state. In this example, the state held in the Redux store would then be a single object containing `auth` and `notes` properties.

There are `counterReducer()` and `authReducer()` functions provided in the code editor, along with a Redux store. Finish writing the `rootReducer()` function using the `Redux.combineReducers()` method. Assign `counterReducer` to a key called `count` and `authReducer` to a key called `auth`.

### Solution:
```jsx
const INCREMENT = 'INCREMENT';
const DECREMENT = 'DECREMENT';

const counterReducer = (state = 0, action) => {
  switch(action.type) {
    case INCREMENT:
      return state + 1;
    case DECREMENT:
      return state - 1;
    default:
      return state;
  }
};

const LOGIN = 'LOGIN';
const LOGOUT = 'LOGOUT';

const authReducer = (state = {authenticated: false}, action) => {
  switch(action.type) {
    case LOGIN:
      return {
        authenticated: true
      }
    case LOGOUT:
      return {
        authenticated: false
      }
    default:
      return state;
  }
};

const rootReducer = Redux.combineReducers({
  count: counterReducer,
  auth: authReducer
})

const store = Redux.createStore(rootReducer);
```

## 11. Send Action Data to the Store
By now you've learned how to dispatch actions to the Redux store, but so far these actions have not contained any information other than a `type`. You can also send specific data along with your actions. In fact, this is very common because actions usually originate from some user interaction and tend to carry some data with them. The Redux store often needs to know about this data.

There's a basic `notesReducer()` and an `addNoteText()` action creator defined in the code editor. Finish the body of the `addNoteText()` function so that it returns an `action` object. The object should include a `type` property with a value of `ADD_NOTE`, and also a `text` property set to the `note` data that's passed into the action creator. When you call the action creator, you'll pass in specific note information that you can access for the object.

Next, finish writing the `switch` statement in the `notesReducer()`. You need to add a case that handles the `addNoteText()` actions. This case should be triggered whenever there is an action of type `ADD_NOTE` and it should return the `text` property on the incoming `action` as the new `state`.

The action is dispatched at the bottom of the code. Once you're finished, run the code and watch the console. That's all it takes to send action-specific data to the store and use it when you update store `state`.

### Solution:
```jsx
const ADD_NOTE = 'ADD_NOTE';

const notesReducer = (state = 'Initial State', action) => {
  switch(action.type) {
    case ADD_NOTE:
      return action.text

    default:
      return state;
  }
};

const addNoteText = (note) => {
  return {
    type: ADD_NOTE,
    text: note
  };

};

const store = Redux.createStore(notesReducer);

console.log(store.getState());
store.dispatch(addNoteText('Hello!'));
console.log(store.getState());
```

## 12. Use Middleware to Handle Asynchronous Actions
So far these challenges have avoided discussing asynchronous actions, but they are an unavoidable part of web development. At some point you'll need to call asynchronous endpoints in your Redux app, so how do you handle these types of requests? Redux provides middleware designed specifically for this purpose, called Redux Thunk middleware. Here's a brief description how to use this with Redux.

To include Redux Thunk middleware, you pass it as an argument to `Redux.applyMiddleware()`. This statement is then provided as a second optional parameter to the `createStore()` function. Take a look at the code at the bottom of the editor to see this. Then, to create an asynchronous action, you return a function in the action creator that takes `dispatch` as an argument. Within this function, you can dispatch actions and perform asynchronous requests.

In this example, an asynchronous request is simulated with a `setTimeout()` call. It's common to dispatch an action before initiating any asynchronous behavior so that your application state knows that some data is being requested (this state could display a loading icon, for instance). Then, once you receive the data, you dispatch another action which carries the data as a payload along with information that the action is completed.

Remember that you're passing `dispatch` as a parameter to this special action creator. This is what you'll use to dispatch your actions, you simply pass the action directly to dispatch and the middleware takes care of the rest.

Write both dispatches in the `handleAsync()` action creator. Dispatch `requestingData()` before the `setTimeout()` (the simulated API call). Then, after you receive the (pretend) data, dispatch the `receivedData()` action, passing in this data. Now you know how to handle asynchronous actions in Redux. Everything else continues to behave as before.

### Solution:
```jsx
const REQUESTING_DATA = 'REQUESTING_DATA'
const RECEIVED_DATA = 'RECEIVED_DATA'

const requestingData = () => { return {type: REQUESTING_DATA} }
const receivedData = (data) => { return {type: RECEIVED_DATA, users: data.users} }

const handleAsync = () => {
  return function(dispatch) {
    // Dispatch request action here
    store.dispatch(requestingData())
    setTimeout(function() {
      let data = {
        users: ['Jeff', 'William', 'Alice']
      }
      // Dispatch received data action here
    store.dispatch(receivedData(data))
    }, 2500);
  }
};

const defaultState = {
  fetching: false,
  users: []
};

const asyncDataReducer = (state = defaultState, action) => {
  switch(action.type) {
    case REQUESTING_DATA:
      return {
        fetching: true,
        users: []
      }
    case RECEIVED_DATA:
      return {
        fetching: false,
        users: action.users
      }
    default:
      return state;
  }
};

const store = Redux.createStore(
  asyncDataReducer,
  Redux.applyMiddleware(ReduxThunk.default)
);
```

## 13. Write a Counter with Redux
Now you've learned all the core principles of Redux! You've seen how to create actions and action creators, create a Redux store, dispatch your actions against the store, and design state updates with pure reducers. You've even seen how to manage complex state with reducer composition and handle asynchronous actions. These examples are simplistic, but these concepts are the core principles of Redux. If you understand them well, you're ready to start building your own Redux app. The next challenges cover some of the details regarding `state` immutability, but first, here's a review of everything you've learned so far.

In this lesson, you'll implement a simple counter with Redux from scratch. The basics are provided in the code editor, but you'll have to fill in the details! Use the names that are provided and define `incAction` and `decAction` action creators, the `counterReducer()`, `INCREMENT` and `DECREMENT` action types, and finally the Redux `store`. Once you're finished you should be able to dispatch `INCREMENT` or `DECREMENT` actions to increment or decrement the state held in the `store`. Good luck building your first Redux app!

### Solution:
```jsx
const INCREMENT = "INCREMENT"; 
// Define a constant for increment action types
const DECREMENT = "DECREMENT"; 
// Define a constant for decrement action types

const counterReducer = (state = 0, action) => {
  switch (action.type) {
    case INCREMENT:
      return state + 1
    case DECREMENT:
      return state - 1
    default:
      return state
  }
}; 
// Define the counter reducer which will increment or 
// decrement the state based on the action it receives

const incAction = () => {
  return {
    type: INCREMENT
  }
}; 
// Define an action creator for incrementing

const decAction = () => {
  return {
    type: DECREMENT
  }
}; 
// Define an action creator for decrementing

const store = Redux.createStore(counterReducer); 
// Define the Redux store here, passing in your reducers
```

## 14. Never Mutate State
These final challenges describe several methods of enforcing the key principle of state immutability in Redux. Immutable state means that you never modify state directly, instead, you return a new copy of state.

If you took a snapshot of the state of a Redux app over time, you would see something like `state 1`, `state 2`, `state 3`,`state 4`, `...` and so on where each state may be similar to the last, but each is a distinct piece of data. This immutability, in fact, is what provides such features as time-travel debugging that you may have heard about.

Redux does not actively enforce state immutability in its store or reducers, that responsibility falls on the programmer. Fortunately, JavaScript (especially ES6) provides several useful tools you can use to enforce the immutability of your state, whether it is a `string`, `number`, `array`, or `object`. Note that strings and numbers are primitive values and are immutable by nature. In other words, 3 is always 3. You cannot change the value of the number 3. An `array` or `object`, however, is mutable. In practice, your state will probably consist of an `array` or `object`, as these are useful data structures for representing many types of information.

There is a `store` and `reducer` in the code editor for managing to-do items. Finish writing the `ADD_TO_DO` case in the reducer to append a new to-do to the state. There are a few ways to accomplish this with standard JavaScript or ES6. See if you can find a way to return a new array with the item from `action.todo` appended to the end.

### Solution:
```jsx
const ADD_TO_DO = 'ADD_TO_DO';

// A list of strings representing tasks to do:
const todos = [
  'Go to the store',
  'Clean the house',
  'Cook dinner',
  'Learn to code',
];

const immutableReducer = (state = todos, action) => {
  switch(action.type) {
    case ADD_TO_DO:
      // Don't mutate state here or the tests will fail
      return state.concat(action.todo)
      // return state
    default:
      return state;
  }
};

const addToDo = (todo) => {
  return {
    type: ADD_TO_DO,
    todo
  }
}

const store = Redux.createStore(immutableReducer);
```

## 15. Use the Spread Operator on Arrays
One solution from ES6 to help enforce state immutability in Redux is the spread operator: `...`. The spread operator has a variety of applications, one of which is well-suited to the previous challenge of producing a new array from an existing array. This is relatively new, but commonly used syntax. For example, if you have an array `myArray` and write:

```js
let newArray = [...myArray];
```

`newArray` is now a clone of `myArray`. Both arrays still exist separately in memory. If you perform a mutation like `newArray.push(5)`, `myArray` doesn't change. The `...` effectively _spreads_ out the values in `myArray` into a new array. To clone an array but add additional values in the new array, you could write `[...myArray, 'new value']`. This would return a new array composed of the values in `myArray` and the string `new value` as the last value. The spread syntax can be used multiple times in array composition like this, but it's important to note that it only makes a shallow copy of the array. That is to say, it only provides immutable array operations for one-dimensional arrays.

Use the spread operator to return a new copy of state when a to-do is added.

### Solution:
```jsx
const immutableReducer = (state = ['Do not mutate state!'], action) => {
  switch(action.type) {
    case 'ADD_TO_DO':
      // Don't mutate state here or the tests will fail
      return [...state, action.todo]
    default:
      return state;
  }
};

const addToDo = (todo) => {
  return {
    type: 'ADD_TO_DO',
    todo
  }
}

const store = Redux.createStore(immutableReducer);
```

## 16. Remove an Item from an Array
Time to practice removing items from an array. The spread operator can be used here as well. Other useful JavaScript methods include `slice()` and `concat()`.

The reducer and action creator were modified to remove an item from an array based on the index of the item. Finish writing the reducer so a new state array is returned with the item at the specific index removed.

### Solution:
```jsx
const immutableReducer = (state = [0,1,2,3,4,5], action) => {
  switch(action.type) {
    case 'REMOVE_ITEM':
      // Don't mutate state here or the tests will fail
      const index = action.index;
      return [
        ...state.slice(0, index),
        ...state.slice(index + 1, state.length)
      ]
    default:
      return state;
  }
};

const removeItem = (index) => {
  return {
    type: 'REMOVE_ITEM',
    index
  }
}

const store = Redux.createStore(immutableReducer);
```

## 17. Copy an Object with `Object.assign`
The last several challenges worked with arrays, but there are ways to help enforce state immutability when state is an `object`, too. A useful tool for handling objects is the `Object.assign()` utility. `Object.assign()` takes a target object and source objects and maps properties from the source objects to the target object. Any matching properties are overwritten by properties in the source objects. This behavior is commonly used to make shallow copies of objects by passing an empty object as the first argument followed by the object(s) you want to copy. Here's an example:

```js
const newObject = Object.assign({}, obj1, obj2);
```

This creates `newObject` as a new `object`, which contains the properties that currently exist in `obj1` and `obj2`.

The Redux state and actions were modified to handle an `object` for the `state`. Edit the code to return a new `state` object for actions with type `ONLINE`, which set the `status` property to the string `online`. Try to use `Object.assign()` to complete the challenge.

### Solution:
```jsx
const defaultState = {
  user: 'CamperBot',
  status: 'offline',
  friends: '732,982',
  community: 'freeCodeCamp'
};

const immutableReducer = (state = defaultState, action) => {
  switch(action.type) {
    case 'ONLINE':
      // Don't mutate state here or the tests will fail
      return Object.assign({}, state, {status: "online"})
    default:
      return state;
  }
};

const wakeUp = () => {
  return {
    type: 'ONLINE'
  }
};

const store = Redux.createStore(immutableReducer);
```


# React and Redux

## 1. Getting Started with React Redux
This series of challenges introduces how to use Redux with React. First, here's a review of some of the key principles of each technology. React is a view library that you provide with data, then it renders the view in an efficient, predictable way. Redux is a state management framework that you can use to simplify the management of your application's state. Typically, in a React Redux app, you create a single Redux store that manages the state of your entire app. Your React components subscribe to only the pieces of data in the store that are relevant to their role. Then, you dispatch actions directly from React components, which then trigger store updates.

Although React components can manage their own state locally, when you have a complex app, it's generally better to keep the app state in a single location with Redux. There are exceptions when individual components may have local state specific only to them. Finally, because Redux is not designed to work with React out of the box, you need to use the `react-redux` package. It provides a way for you to pass Redux `state` and `dispatch` to your React components as `props`.

Over the next few challenges, first, you'll create a simple React component which allows you to input new text messages. These are added to an array that's displayed in the view. This should be a nice review of what you learned in the React lessons. Next, you'll create a Redux store and actions that manage the state of the messages array. Finally, you'll use `react-redux` to connect the Redux store with your component, thereby extracting the local state into the Redux store.

Start with a `DisplayMessages` component. Add a constructor to this component and initialize it with a state that has two properties: `input`, that's set to an empty string, and `messages`, that's set to an empty array.

### Solution:
```jsx
class DisplayMessages extends React.Component {

  constructor(props) {
    super(props);
    this.state = {
      input: '',
      messages: []
    }
  }
  render() {
    return <div />
  }
};
```

## 2. Manage State Locally First
Here you'll finish creating the `DisplayMessages` component.

First, in the `render()` method, have the component render an `input` element, `button` element, and `ul` element. When the `input` element changes, it should trigger a `handleChange()` method. Also, the `input` element should render the value of `input` that's in the component's state. The `button` element should trigger a `submitMessage()` method when it's clicked.

Second, write these two methods. The `handleChange()` method should update the `input` with what the user is typing. The `submitMessage()` method should concatenate the current message (stored in `input`) to the `messages` array in local state, and clear the value of the `input`.

Finally, use the `ul` to map over the array of `messages` and render it to the screen as a list of `li` elements.

### Solution:
```jsx
class DisplayMessages extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      messages: []
    }
    this.handleChange = this.handleChange.bind(this);
    this.submitMessage = this.submitMessage.bind(this);
  }
  
  handleChange(event) {
    this.setState({
      input: event.target.value
    })
  }

  submitMessage() {
    this.setState({
      input: "",
      messages: [...this.state.messages, this.state.input]
    })
  }

  render() {
    return (
      <div>
        <h2>Type in a new Message:</h2>
        <input value={this.state.input} onChange={this.handleChange}></input>
        <button onClick={this.submitMessage}>Add message</button>
        <ul>
          {this.state.messages.map(message => {
            return (
              <li>{message}</li>
            )
          })}
        </ul>
      </div>
    );
  }
};
```

## 3. Extract State Logic to Redux
Now that you finished the React component, you need to move the logic it's performing locally in its `state` into Redux. This is the first step to connect the simple React app to Redux. The only functionality your app has is to add new messages from the user to an unordered list. The example is simple in order to demonstrate how React and Redux work together.

First, define an action type `ADD` and set it to a const `ADD`. Next, define an action creator `addMessage()` which creates the action to add a message. You'll need to pass a `message` to this action creator and include the message in the returned `action`.

Then create a reducer called `messageReducer()` that handles the state for the messages. The initial state should equal an empty array. This reducer should add a message to the array of messages held in state, or return the current state. Finally, create your Redux store and pass it the reducer.

### Solution:
```jsx
const ADD = "ADD";

const messageReducer = (state = [], action) => {
  switch(action.type) {
    case ADD:
      return [...state, action.message]
    default:
      return state
  }
}

const addMessage = (message) => {
  return {
    type: ADD,
    message
  }
}

const store = Redux.createStore( messageReducer)
```

## 4. Use Provider to Connect Redux to React
In the last challenge, you created a Redux store to handle the messages array and created an action for adding new messages. The next step is to provide React access to the Redux store and the actions it needs to dispatch updates. React Redux provides its `react-redux` package to help accomplish these tasks.

React Redux provides a small API with two key features: `Provider` and `connect`. Another challenge covers `connect`. The `Provider` is a wrapper component from React Redux that wraps your React app. This wrapper then allows you to access the Redux `store` and `dispatch` functions throughout your component tree. `Provider` takes two props, the Redux store and the child components of your app. Defining the `Provider` for an App component might look like this:

```jsx
<Provider store={store}>
  <App/>
</Provider>
```

The code editor now shows all your Redux and React code from the past several challenges. It includes the Redux store, actions, and the `DisplayMessages` component. The only new piece is the `AppWrapper` component at the bottom. Use this top level component to render the `Provider` from `ReactRedux`, and pass the Redux store as a prop. Then render the `DisplayMessages` component as a child. Once you are finished, you should see your React component rendered to the page.

**Note:** React Redux is available as a global variable here, so you can access the Provider with dot notation. The code in the editor takes advantage of this and sets it to a constant `Provider` for you to use in the `AppWrapper` render method.

### Solution:
```jsx
// Redux:
const ADD = 'ADD';

const addMessage = (message) => {
  return {
    type: ADD,
    message
  }
};

const messageReducer = (state = [], action) => {
  switch (action.type) {
    case ADD:
      return [
        ...state,
        action.message
      ];
    default:
      return state;
  }
};

const store = Redux.createStore(messageReducer);


// React:

class DisplayMessages extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      messages: []
    }
    this.handleChange = this.handleChange.bind(this);
    this.submitMessage = this.submitMessage.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  submitMessage() {  
    this.setState((state) => {
      const currentMessage = state.input;
      return {
        input: '',
        messages: state.messages.concat(currentMessage)
      };
    });
  }
  render() {
    return (
      <div>
        <h2>Type in a new Message:</h2>
        <input
          value={this.state.input}
          onChange={this.handleChange}/><br/>
        <button onClick={this.submitMessage}>Submit</button>
        <ul>
          {this.state.messages.map( (message, idx) => {
              return (
                 <li key={idx}>{message}</li>
              )
            })
          }
        </ul>
      </div>
    );
  }
};

const Provider = ReactRedux.Provider;

class AppWrapper extends React.Component {
  render(){
    return (
      <Provider store={store}>
        <DisplayMessages/>
      </Provider>
    )
  }
};
```

## 5. Map State to Props
The `Provider` component allows you to provide `state` and `dispatch` to your React components, but you must specify exactly what state and actions you want. This way, you make sure that each component only has access to the state it needs. You accomplish this by creating two functions: `mapStateToProps()` and `mapDispatchToProps()`.

In these functions, you declare what pieces of state you want to have access to and which action creators you need to be able to dispatch. Once these functions are in place, you'll see how to use the React Redux `connect` method to connect them to your components in another challenge.

**Note:** Behind the scenes, React Redux uses the `store.subscribe()` method to implement `mapStateToProps()`.

Create a function `mapStateToProps()`. This function should take `state` as an argument, then return an object which maps that state to specific property names. These properties will become accessible to your component via `props`. Since this example keeps the entire state of the app in a single array, you can pass that entire state to your component. Create a property `messages` in the object that's being returned, and set it to `state`.

### Solution:
```jsx
const state = [];

const mapStateToProps = (state) => {
  return {
    messages: state
  }
}
```

## 6. Map Dispatch to Props
The `mapDispatchToProps()` function is used to provide specific action creators to your React components so they can dispatch actions against the Redux store. It's similar in structure to the `mapStateToProps()` function you wrote in the last challenge. It returns an object that maps dispatch actions to property names, which become component `props`. However, instead of returning a piece of `state`, each property returns a function that calls `dispatch` with an action creator and any relevant action data. You have access to this `dispatch` because it's passed in to `mapDispatchToProps()` as a parameter when you define the function, just like you passed `state` to `mapStateToProps()`. Behind the scenes, React Redux is using Redux's `store.dispatch()` to conduct these dispatches with `mapDispatchToProps()`. This is similar to how it uses `store.subscribe()` for components that are mapped to `state`.

For example, you have a `loginUser()` action creator that takes a `username` as an action payload. The object returned from `mapDispatchToProps()` for this action creator would look something like:

```jsx
{
  submitLoginUser: function(username) {
    dispatch(loginUser(username));
  }
}
```

The code editor provides an action creator called `addMessage()`. Write the function `mapDispatchToProps()` that takes `dispatch` as an argument, then returns an object. The object should have a property `submitNewMessage` set to the dispatch function, which takes a parameter for the new message to add when it dispatches `addMessage()`.

### Solution:
```jsx
const addMessage = (message) => {
  return {
    type: 'ADD',
    message: message
  }
};

// Change code below this line
const mapDispatchToProps = (dispatch) => {
  return {
    submitNewMessage: function(message) {
      dispatch(addMessage(message))
    }
  }
}
```

## 7. Connect Redux to React
Now that you've written both the `mapStateToProps()` and the `mapDispatchToProps()` functions, you can use them to map `state` and `dispatch` to the `props` of one of your React components. The `connect` method from React Redux can handle this task. This method takes two optional arguments, `mapStateToProps()` and `mapDispatchToProps()`. They are optional because you may have a component that only needs access to `state` but doesn't need to dispatch any actions, or vice versa.

To use this method, pass in the functions as arguments, and immediately call the result with your component. This syntax is a little unusual and looks like:

```js
connect(mapStateToProps, mapDispatchToProps)(MyComponent)
```

**Note:** If you want to omit one of the arguments to the `connect` method, you pass `null` in its place.

The code editor has the `mapStateToProps()` and `mapDispatchToProps()` functions and a new React component called `Presentational`. Connect this component to Redux with the `connect` method from the `ReactRedux` global object, and call it immediately on the `Presentational` component. Assign the result to a new `const` called `ConnectedComponent` that represents the connected component. That's it, now you're connected to Redux! Try changing either of `connect`'s arguments to `null` and observe the test results.

### Solution:
```jsx
const addMessage = (message) => {
  return {
    type: 'ADD',
    message: message
  }
};

const mapStateToProps = (state) => {
  return {
    messages: state
  }
};

const mapDispatchToProps = (dispatch) => {
  return {
    submitNewMessage: (message) => {
      dispatch(addMessage(message));
    }
  }
};

class Presentational extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <h3>This is a Presentational Component</h3>
  }
};

const connect = ReactRedux.connect;
// Change code below this line
const ConnectedComponent = connect(mapStateToProps, mapDispatchToProps)(Presentational)
```

## 8. Connect Redux to the Messages App
Now that you understand how to use `connect` to connect React to Redux, you can apply what you've learned to your React component that handles messages.

In the last lesson, the component you connected to Redux was named `Presentational`, and this wasn't arbitrary. This term _generally_ refers to React components that are not directly connected to Redux. They are simply responsible for the presentation of UI and do this as a function of the props they receive. By contrast, container components are connected to Redux. These are typically responsible for dispatching actions to the store and often pass store state to child components as props.

The code editor has all the code you've written in this section so far. The only change is that the React component is renamed to `Presentational`. Create a new component held in a constant called `Container` that uses `connect` to connect the `Presentational` component to Redux. Then, in the `AppWrapper`, render the React Redux `Provider` component. Pass `Provider` the Redux `store` as a prop and render `Container` as a child. Once everything is set up, you will see the messages app rendered to the page again.

### Solution:
```jsx
// Redux:
const ADD = 'ADD';

const addMessage = (message) => {
  return {
    type: ADD,
    message: message
  }
};

const messageReducer = (state = [], action) => {
  switch (action.type) {
    case ADD:
      return [
        ...state,
        action.message
      ];
    default:
      return state;
  }
};

const store = Redux.createStore(messageReducer);

// React:
class Presentational extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      messages: []
    }
    this.handleChange = this.handleChange.bind(this);
    this.submitMessage = this.submitMessage.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  submitMessage() {
    this.setState((state) => {
      const currentMessage = state.input;
      return {
        input: '',
        messages: state.messages.concat(currentMessage)
      };
    });
  }
  render() {
    return (
      <div>
        <h2>Type in a new Message:</h2>
        <input
          value={this.state.input}
          onChange={this.handleChange}/><br/>
        <button onClick={this.submitMessage}>Submit</button>
        <ul>
          {this.state.messages.map( (message, idx) => {
              return (
                 <li key={idx}>{message}</li>
              )
            })
          }
        </ul>
      </div>
    );
  }
};

// React-Redux:
const mapStateToProps = (state) => {
  return { messages: state }
};

const mapDispatchToProps = (dispatch) => {
  return {
    submitNewMessage: (newMessage) => {
       dispatch(addMessage(newMessage))
    }
  }
};

const Provider = ReactRedux.Provider;
const connect = ReactRedux.connect;

// Define the Container component here:
const Container = connect(mapStateToProps, mapDispatchToProps)(Presentational)

class AppWrapper extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    // Complete the return statement:
    return (
	    <Provider store={store}>
	      <Container/>
	    </Provider>
    );
  }
};
```

## 9. Extract Local State into Redux
You're almost done! Recall that you wrote all the Redux code so that Redux could control the state management of your React messages app. Now that Redux is connected, you need to extract the state management out of the `Presentational` component and into Redux. Currently, you have Redux connected, but you are handling the state locally within the `Presentational` component.

In the `Presentational` component, first, remove the `messages` property in the local `state`. These messages will be managed by Redux. Next, modify the `submitMessage()` method so that it dispatches `submitNewMessage()` from `this.props`, and pass in the current message input from local `state` as an argument. Because you removed `messages` from local state, remove the `messages` property from the call to `this.setState()` here as well. Finally, modify the `render()` method so that it maps over the messages received from `props` rather than `state`.

Once these changes are made, the app will continue to function the same, except Redux manages the state. This example also illustrates how a component may have local `state`: your component still tracks user input locally in its own `state`. You can see how Redux provides a useful state management framework on top of React. You achieved the same result using only React's local state at first, and this is usually possible with simple apps. However, as your apps become larger and more complex, so does your state management, and this is the problem Redux solves.

### Solution:
```jsx
// Redux:
const ADD = 'ADD';

const addMessage = (message) => {
  return {
    type: ADD,
    message: message
  }
};

const messageReducer = (state = [], action) => {
  switch (action.type) {
    case ADD:
      return [
        ...state,
        action.message
      ];
    default:
      return state;
  }
};

const store = Redux.createStore(messageReducer);

// React:
const Provider = ReactRedux.Provider;
const connect = ReactRedux.connect;

// Change code below this line
class Presentational extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
    }
    this.handleChange = this.handleChange.bind(this);
    this.submitMessage = this.submitMessage.bind(this);
  }
  handleChange(event) {
    this.setState({
      input: event.target.value
    });
  }
  submitMessage() {
    this.props.submitNewMessage(this.state.input)
    this.setState(() => ({
      input: ''
    }));
  }
  render() {
    return (
      <div>
        <h2>Type in a new Message:</h2>
        <input
          value={this.state.input}
          onChange={this.handleChange}/><br/>
        <button onClick={this.submitMessage}>Submit</button>
        <ul>
          {this.props.messages.map( (message, idx) => {
              return (
                 <li key={idx}>{message}</li>
              )
            })
          }
        </ul>
      </div>
    );
  }
};
// Change code above this line

const mapStateToProps = (state) => {
  return {messages: state}
};

const mapDispatchToProps = (dispatch) => {
  return {
    submitNewMessage: (message) => {
      dispatch(addMessage(message))
    }
  }
};

const Container = connect(mapStateToProps, mapDispatchToProps)(Presentational);

class AppWrapper extends React.Component {
  render() {
    return (
      <Provider store={store}>
        <Container/>
      </Provider>
    );
  }
};
```

## 10. Moving Forward From Here
Congratulations! You finished the lessons on React and Redux. There's one last item worth pointing out before you move on. Typically, you won't write React apps in a code editor like this. This challenge gives you a glimpse of what the syntax looks like if you're working with npm and a file system on your own machine. The code should look similar, except for the use of `import` statements (these pull in all of the dependencies that have been provided for you in the challenges). The "Managing Packages with npm" section covers npm in more detail.

Finally, writing React and Redux code generally requires some configuration. This can get complicated quickly. If you are interested in experimenting on your own machine, the [Create React App](https://www.freecodecamp.org/news/install-react-with-create-react-app/) comes configured and ready to go.

Alternatively, you can enable Babel as a JavaScript Preprocessor in CodePen, add React and ReactDOM as external JavaScript resources, and work there as well.

Log the message `'Now I know React and Redux!'` to the console.

# Mini Projects

## 1. Build a Random Quote Machine
**Objective:** Build an app that is functionally similar to this: [Demo](https://random-quote-machine.freecodecamp.rocks/).

Fulfill the below user stories and get all of the tests to pass. Use whichever libraries or APIs you need. Give it your own personal style.

You can use any mix of HTML, JavaScript, CSS, Bootstrap, SASS, React, Redux, and jQuery to complete this project. You should use a frontend framework (like React for example) because this section is about learning frontend frameworks. Additional technologies not listed above are not recommended and using them is at your own risk. We are looking at supporting other frontend frameworks like Angular and Vue, but they are not currently supported. We will accept and try to fix all issue reports that use the suggested technology stack for this project. Happy coding!

**User Story #1:** I can see a wrapper element with a corresponding `id="quote-box"`.

**User Story #2:** Within `#quote-box`, I can see an element with a corresponding `id="text"`.

**User Story #3:** Within `#quote-box`, I can see an element with a corresponding `id="author"`.

**User Story #4:** Within `#quote-box`, I can see a clickable element with a corresponding `id="new-quote"`.

**User Story #5:** Within `#quote-box`, I can see a clickable `a` element with a corresponding `id="tweet-quote"`.

**User Story #6:** On first load, my quote machine displays a random quote in the element with `id="text"`.

**User Story #7:** On first load, my quote machine displays the random quote's author in the element with `id="author"`.

**User Story #8:** When the `#new-quote` button is clicked, my quote machine should fetch a new quote and display it in the `#text` element.

**User Story #9:** My quote machine should fetch the new quote's author when the `#new-quote` button is clicked and display it in the `#author` element.

**User Story #10:** I can tweet the current quote by clicking on the `#tweet-quote` `a` element. This `a` element should include the `"twitter.com/intent/tweet"` path in its `href` attribute to tweet the current quote.

**User Story #11:** The `#quote-box` wrapper element should be horizontally centered. Please run tests with browser's zoom level at 100% and page maximized.

You can build your project by [using this CodePen template](https://codepen.io/pen?template=MJjpwO) and clicking `Save` to create your own pen. Or you can use this CDN link to run the tests in any environment you like: `https://cdn.freecodecamp.org/testable-projects-fcc/v1/bundle.js`

Once you're done, submit the URL to your working project with all its tests passing.

**Note:** Twitter does not allow links to be loaded in an iframe. Try using the `target="_blank"` or `target="_top"` attribute on the `#tweet-quote` element if your tweet won't load. `target="_top"` will replace the current tab so make sure your work is saved.

### Solution:
```jsx
import React, { setState } from "react"
import "react-bootstrap"
import './App.css'

const quotes = [
  {
		id: 1,
		quote: "I have just three things to teach: simplicity, patience, compassion. These three are your greatest treasures.",
		author: "Lao Tzu"
	},
	{
		id: 2,
		quote: "Do today what others won't and achieve tomorrow what others can't.",
		author: "Jerry Rice"
	},
	{
		id: 3,
		quote: "In character, in manner, in style, in all things, the supreme excellence is simplicity.",
		author: "Henry Wadsworth Longfellow"
	},
	{
		id: 4,
		quote: "If we don't discipline ourselves, the world will do it for us.",
		author: "William Feather"
	},
	{
		id: 5,
		quote: "Rule your mind or it will rule you.",
		author: "Horace"
	},
	{
		id: 6,
		quote: "All that we are is the result of what we have thought.",
		author: "Buddha"
	},
	{
		id: 7,
		quote: "Doing just a little bit during the time we have available puts you that much further ahead than if you took no action at all.",
		author: "Pulsifer, Take Action; Don't Procrastinate"
	},
	{
		id: 8,
		quote: "Never leave that till tomorrow which you can do today.",
		author: "Benjamin Franklin"
	},
	{
		id: 9,
		quote: "Procrastination is like a credit card: it's a lot of fun until you get the bill.",
		author: "Christopher Parker"
	},
	{
		id: 10,
		quote: "Someday is not a day of the week.",
		author: "Author Unknown"
	},
	{
		id: 11,
		quote: "Tomorrow is often the busiest day of the week.",
		author: "Spanish Proverb"
	},
	{
		id: 12,
		quote: "I can accept failure, everyone fails at something. But I can't accept not trying.",
		author: "Michael Jordan"
	},
	{
		id: 13,
		quote: "There’s a myth that time is money. In fact, time is more precious than money. It’s a nonrenewable resource. Once you’ve spent it, and if you’ve spent it badly, it’s gone forever.",
		author: "Neil A. Fiore"
	},
	{
		id: 14,
		quote: "Nothing can stop the man with the right mental attitude from achieving his goal; nothing on earth can help the man with the wrong mental attitude.",
		author: "Thomas Jefferson"
	},
	{
		id: 15,
		quote: "There is only one success--to be able to spend your life in your own way.",
		author: "Christopher Morley"
	},
	{
		id: 16,
		quote: "Success is the good fortune that comes from aspiration, desperation, perspiration and inspiration.",
		author: "Evan Esar"
	},
	{
		id: 17,
		quote: "We are still masters of our fate. We are still captains of our souls.",
		author: "Winston Churchill"
	},
	{
		id: 18,
		quote: "Our truest life is when we are in dreams awake.",
		author: "Henry David Thoreau"
	},
	{
		id: 19,
		quote: "The best way to make your dreams come true is to wake up.",
		author: "Paul Valery"
	},
	{
		id: 20,
		quote: "Life without endeavor is like entering a jewel mine and coming out with empty hands.",
		author: "Japanese Proverb"
	},
	{
		id: 21,
		quote: "Happiness does not consist in pastimes and amusements but in virtuous activities.",
		author: "Aristotle"
	},
	{
		id: 22,
		quote: "By constant self-discipline and self-control, you can develop greatness of character.",
		author: "Grenville Kleiser"
	},
	{
		id: 23,
		quote: "The difference between a successful person and others is not a lack of strength, not a lack of knowledge, but rather a lack in will.",
		author: "Vince Lombardi Jr."
	},
	{
		id: 24,
		quote: "At the end of the day, let there be no excuses, no explanations, no regrets.",
		author: "Steve Maraboli"
	},
	{
		id: 25,
		quote: "Inaction will cause a man to sink into the slough of despond and vanish without a trace.",
		author: "Farley Mowat"
	},
]

class App extends React.Component {
  constructor(props) {
    super(props);
    var selectQuote = Math.floor(Math.random() * quotes.length)
    this.state = {
      quote: quotes[selectQuote].quote,
      author: quotes[selectQuote].author
    }

    this.generateQuote = this.generateQuote.bind(this);
  }

  generateQuote = () => {
    var selectQuote = Math.floor(Math.random() * quotes.length)
    this.setState({
      quote: quotes[selectQuote].quote,
      author: quotes[selectQuote].author
    });
  }

  render() {
    return (
      <main className="container-fluid center">
        <div className='row d-flex justify-content-center align-items-center h-300'>
          <h1>Random Quotes Generator</h1>
          
            <div className="card container py-5 h-100" id="quote-box" style={{borderRadius:14}}>
              <div className="card-body">
                <figure>
                  <blockquote className='card-text' id="text">{this.state.quote}</blockquote>
                  <figcaption className='' id="author">{this.state.author}</figcaption>
                </figure>
                <div className="col">
                  <a href="twitter.com/intent/tweet?text={}" target="_blank" id="tweet-quote" className="btn btn-info" onClick={this.generateQuote}>twitter</a>
                  <button id="new-quote" className="btn btn-primary" onClick={this.generateQuote}>Generate Quote</button>
                </div>
              </div>
            </div>
          
        </div>
      </main>
    );
  }
}

export default App;

```

## 2. Build a Markdown Previewer
**Objective:** Build an app that is functionally similar to this: [https://markdown-previewer.freecodecamp.rocks/](https://markdown-previewer.freecodecamp.rocks/).

Fulfill the below user stories and get all of the tests to pass. Use whichever libraries or APIs you need. Give it your own personal style.

You can use any mix of HTML, JavaScript, CSS, Bootstrap, SASS, React, Redux, and jQuery to complete this project. You should use a frontend framework (like React for example) because this section is about learning frontend frameworks. Additional technologies not listed above are not recommended and using them is at your own risk. We are looking at supporting other frontend frameworks like Angular and Vue, but they are not currently supported. We will accept and try to fix all issue reports that use the suggested technology stack for this project. Happy coding!

**User Story #1:** I can see a `textarea` element with a corresponding `id="editor"`.

**User Story #2:** I can see an element with a corresponding `id="preview"`.

**User Story #3:** When I enter text into the `#editor` element, the `#preview` element is updated as I type to display the content of the textarea.

**User Story #4:** When I enter GitHub flavored markdown into the `#editor` element, the text is rendered as HTML in the `#preview` element as I type (HINT: You don't need to parse Markdown yourself - you can import the Marked library for this: [https://cdnjs.com/libraries/marked](https://cdnjs.com/libraries/marked)).

**User Story #5:** When my markdown previewer first loads, the default text in the `#editor` field should contain valid markdown that represents at least one of each of the following elements: a heading element (H1 size), a sub heading element (H2 size), a link, inline code, a code block, a list item, a blockquote, an image, and bolded text.

**User Story #6:** When my markdown previewer first loads, the default markdown in the `#editor` field should be rendered as HTML in the `#preview` element.

**Optional Bonus (you do not need to make this test pass):** My markdown previewer interprets carriage returns and renders them as `br` (line break) elements.

You can build your project by [using this CodePen template](https://codepen.io/pen?template=MJjpwO) and clicking `Save` to create your own pen. Or you can use this CDN link to run the tests in any environment you like: `https://cdn.freecodecamp.org/testable-projects-fcc/v1/bundle.js`

Once you're done, submit the URL to your working project with all its tests passing.