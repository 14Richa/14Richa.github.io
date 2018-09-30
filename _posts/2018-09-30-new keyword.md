---
layout: post
title:  "Requirements when creating a User Defined objects"
author: "Richa"
---


While creating a user-defined objects there are two steps which are required:

1. Defining the object type by writing a function.
2. Creating an object with 'new' keyword.

To define an object type we have to create a function for the object type that focus on its name and properties.

The 'new' keyword creates a case of a user-defined object or  built-in object  that has a constructor function.

Example: 
{% highlight js %}

function Scooter(make, model, year) {
this.make = make;
this.model = model;
this.year = year;
}

var scooter1 = new Scooter('Activa', 'XXX3', 1996);

console.log(car1.year); // 1996


{% endhighlight %}

