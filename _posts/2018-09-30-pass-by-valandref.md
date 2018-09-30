---
layout: post
title:  "Passing value or reference??"
author: "Richa"
---

# Pass By Value

In Pass by Value, functions are called directly by passing the value of the variable in the form of argument. 

If programmer changes the argument inside the function it doesn't affect the variable which is globally passes or is outside the function.

Javascript often pass by value,  so if someone changes the value of the variable; the basic or primary value will not get changed (String or number).

Example: 
{% highlight js %}

function idea(ideaOne, ideaTwo) {
console.log ("Inside the idea function"); // Inside the idea function
ideaOne = 340;
ideaTwo = 140;
console.log("ideaOne =" + ideaOne +"ideaTwo =" +ideaTwo); // ideaOne = 340 ideaTwo = 140
}

let ideaOne = 300;
let ideaTwo = 200;

console.log("ideaOne =" +ideaOne + "ideaTwo =" +ideaTwo); // ideaOne = 300; ideaTwo = 200

idea(ideaOne, ideaTwo); 
// Inside the idea function
// ideaOne = 340 ideaTwo = 140

console.log("ideaOne =" +ideaOne + "ideaTwo =" +ideaTwo); // ideaOne = 300; ideaTwo = 200

{% endhighlight %}


# Pass By Reference

Basics data types in Javascript like number, string and boolean  pass by value whereas data types like objects and arrays are pass by reference.

In Pass by Reference, functions are called by directly passing the address of the variable as the argument. Changing the argument inside the function affects the variable which is passed from outside the function.

Example:

{% highlight js %}

function idea(ideaObj) {
console.log("Inside the idea function"); // Inside the idea function
ideaObj.x = 250; 
console.log(ideaObj); // { x : 250 }
}

let ideaObj = { x : 200 };

console.log(ideaObj); // { x : 200 }

idea(ideaObj)

    // Inside the idea function
   // { x : 250 }

console.log(ideaObj); // { x : 250 };

{% endhighlight %}
