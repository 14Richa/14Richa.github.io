---
layout: post
title:  "Let, Var and Const"
author: "Richa"
---

This blog consist the scope and use of `var`, `let` and `const` in Javascript. 
Three of the above methods are used to define a variable in Javascript but three of them hold a different properties and scope which vary their usage in a function.

# Scope of Var 

Scope means in simple language that where the particular variables can be used.

`Var` has a global scope.
 That means that any variable that is declared with var outside a function block can be used in the whole function.

 {% highlight js %}
// Example
var x = 1;

if (x == 1) {
  var x = 2;

  console.log(x);
  //Prints 2
}

console.log(x);
//Prints 2
{% endhighlight %}

# Scope Of Let

Anything within `{}` is a block. 
So a variable declared in a block with the `let` is only used within that block.

{% highlight js %}
// Example
let a = 10;
If(true){
	let a = 5;
	let b = 20;
	console.log(a); //Prints 5
	console.log(b); //Prints 20
}
console.log(a); //Prints 10
console.log(b); //Undefined

{% endhighlight %}

# Scope of Const 

Variables declared with the `const` maintain a fixed values. 
`const`  declarations share same similarities as let declarations.

Like `let` declarations, `const` declarations can only be used within the block it is declared.

{% highlight js %}
// Example
var x = 10;
// Here x value is 10
{ 
    const x = 2;
    // Here x value is 2
}
// Here x value is 10

{% endhighlight %}
