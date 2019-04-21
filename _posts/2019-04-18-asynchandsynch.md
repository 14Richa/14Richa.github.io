---
layout: post
title:  "Sync Programming and Async Programming"
author: "Richa"
---

I was recently asked this question in an interview. I decided to get to the bottom of this.

When you write code in any of the high-level languages (Python, Javascript, Scala etc.), the program execution is very straightforward. Your program starts at the top and executes one line at a time, and the next line is executed when the previous line's execution finishes. This is called Synchronous program execution. Each time a code block or a function is called, the program waits for until that code-block is successfully executed or until that function returns before moving to the next line of code. This is good and easy to understand but can have undesirable ramifications. Suppose if a function is time-consuming then your process is stuck while that function runs.

Asynchronous execution avoids this problem. It is something like saying that let us proceed with the part of the code that doesn't require output of the time consuming function and we will return to the functions which require the output when we do have that output, i.e we will call-back the functions dependent on the time-consuming function's output when it has completed.

This brings us to callback functions.

## Callback functions

Simply put — when a function has another function as an argument, that argument function is known as a callback function. This is because that function in not directly called upon but is called-back upon when the higher order function is executed
 {% highlight js %}
    
    function introduction(firstName, lastName, callback) {
      const fullName = ${firstName} ${lastName};
    
      callback(fullName);
    }
    
    introduction('Chris','Nwamba', greeting); // Hello Chris Nwamba, welcome to Scotch!
{% endhighlight %}

This means when we use functions with array methods like map, filter etc. those are also callback functions.

But one of the main applications of callback functions we see are when we want to call the functions dependent on execution of a time-consuming main function. Adding event listeners in a browser with `addEventListener`, reading files `fs.readFile` are examples of common APIs that uses callbacks.

Let us see an example of callback functions in action. I have used the same examples as in this very good [blogpost by Sebastian Lindström.](https://medium.com/codebuddies/getting-to-know-asynchronous-javascript-callbacks-promises-and-async-await-17e0673281ee)
{% highlight js %}

    const request = require(‘request’);
    function handleResponse(error, response, body){
        if(error){
            // Handle error.
        }
        else {
            // Successful, do something with the result.
        }
    }
    request('<https://www.somepage.com>', handleResponse);

{% endhighlight %}

The last argument of `request` is a callback function `handleResponse`. We can also pass anonymous/arrow functions in the call directly. This function is not executed together with the code but is executed later once the underlying I/O operation is done.

This is all neat and tidy. But what if we want to do multiple operations with the data and based on the data received might want to fetch more data. Again I will use the example for the [same blogpost](https://medium.com/codebuddies/getting-to-know-asynchronous-javascript-callbacks-promises-and-async-await-17e0673281ee).
{% highlight js %}

    request('<http://www.somepage.com>', function (firstError, firstResponse, firstBody) {
        if(firstError){
            // Handle error.
        }
        else {
            request(`http://www.somepage.com/${firstBody.someValue}`, function (secondError, secondResponse, secondBody) {
                if(secondError){
                    // Handle error.
                }
                else {
                    // Use secondBody for something
                }
            });
        }
    });

{% endhighlight %}


What we see above is a nested callback code block. This soon gets messy and is popularly called callback hell. This has been discussed at length here, here and here.

How do we get out of this?

# Promises

A promise is an asynchronous operation that may complete at some point and produce a value. It is exported as a new kind of object in Javascript that wraps an async operation and notifies when it's done.

Instead of passing another function which will be called back, promise object has a new interface which gives you option to write the callback functions succinctly inside the `then` tags and reads much better than the nested callback code blocks.

It is easier to understand with an example, let us borrow another one from [the blogpost](https://medium.com/codebuddies/getting-to-know-asynchronous-javascript-callbacks-promises-and-async-await-17e0673281ee).
{% highlight js %}

    const axios = require(‘axios’);
    
    axios.get(‘<http://www.somepage.com>')
    .then(function (response) { // Reponse being the result of the first request
        // Returns another promise to the next .then(..) in the chain
        return axios.get(`http://www.somepage.com/${response.someValue}`);
    })
    .then(function response { // Reponse being the result of the second request
        // Handle response
    })
    .catch(function (error) {
        // Handle error.
    });

{% endhighlight %}


So the above code blocks achieves the same output as the one with nested callbacks but is much easy to read, follow and debug. Crux of the matter is that a nested callback code-block can be transformed to a chain of `then()` tags when writing with promises.

Couple of points to highlight:

1. Code in each `then()` tag is executed when either the request has finished or the previous `then()` tag has finished execution;
2. There is only one `catch()` to handle errors from all `then()` calls;
3. Every `then()` call should return a new Promise object or a value.

Now we understand how `Promises` work and how they can be used to replace callbacks. In another post I would try to explain how to create new promise objects and also modify callback based API calls to work with `Promise` interface.

Ta-da!





