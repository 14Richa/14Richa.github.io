---
layout: post
title:  "Classes V/s Ids"
author: "Richa"
---

### Classes are NOT unique

  1. You can use the same class on multiple elements.
  2. You can use multiple classes on the same element.
    
 Any styling information that needs to be applied to multiple objects on a page should be done with a class. Take for example a page with multiple "widgets":

`<div class="widget"></div>
<div class="widget"></div>
<div class="widget"></div>`

You can now use the class name "widget" as your hook to apply the same set of styling to each one of these. But what if you need one of them to be bigger than the other, but still share all the other attributes? Classes has you covered there, as you can apply more than one class:

`<div class="widget"></div>
<div class="widget big"></div>
<div class="widget"></div>`

No need to make a brand new class name here, just apply a new class right in the class attribute.


### Id's are unique

 1. Each element can have only one ID

 2. Each page can have only one element with that ID

  When I was first learning this stuff, I heard over and over that you should only use ID's once, but you can use classes over and over.  If you are purely an HTML/CSS person, this attitude can continue because to you, they really don't seem to do anything different.

 `Your code will not pass validation if you use the same ID on more than one element.`



### Elements can have BOTH


There is nothing stopping you from having both an ID and a Class on a single element. In fact, it is often a very good idea. 

 Example:

`<li id="comment" class="item">`

It has a class applied to it that you may want for styling all comments on the page, but it also has a unique ID value. This ID value is useful for direct linking. 

Now, I can link directly to a particular comment on a particular page easily.


### CSS doesn't care

Regarding CSS, there is nothing you can do with an ID that you can't do with a Class and vice versa. I remember when I was first learning CSS and I was having a problem, sometimes I would try and troubleshoot by switching around these values. Nope. CSS doesn't care.

### Javascript cares

JavaScript people are already probably more in tune with the differences between classes and ID's. JavaScript depends on there being only one page element with any particular id, or else the commonly used (getElementByIdfunction) wouldn't be dependable. 
