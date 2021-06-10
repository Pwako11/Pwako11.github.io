---
layout: post
title:      "Asynchronous actions, Promises and Fetch"
date:       2021-06-01 04:14:52 +0000
permalink:  asynchronous_actions_promises_and_fetch
---

Working with abstract concepts is often easier when those concepts can be represented by values. In the case of asynchronous actions, you could, instead of arranging for a function to be called at some point in the future, return an object that represents this future event, this is where promises come into play. The term asynchronous refers to two or more objects or events not existing or happening at the same time (or multiple related things happening without waiting for the previous one to complete). A promise is an Asynchronous action that may be completed at some point and produce a value. A Promise is an object that's returned by a function that has not yet completed its work. The promise literally represents a promise made by the function that it will eventually return a result through the promise object. it is able to notify anyone  who is interested when its value is available.  When the called function finishes its work asynchronously, a function on the promise object called a resolution (or fulfillment, or completion) handler is called to let the original caller know that the task is complete. When working wit API's Javascript uses Asynchronous actions coupled with promises and fetch functions to complete network calls while still other work orders to the DOM. 
The Fetch API provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses. It also provides a global fetch() method that provides an easy, logical way to fetch resources asynchronously across the network

The term asynchronous refers to two or more objects or events not existing or happening at the same time (or multiple related things happening without waiting for the previous one to complete). In computing, the word "asynchronous" is used in two major contexts; `Networking and communications` and `Software design`. Asynchronous software design expands upon the concept by building code that allows a program to ask that a task be performed alongside the original task (or tasks), without stopping to wait for the task to complete. When the secondary task is completed, the original task is notified using an agreed-upon mechanism so that it knows the work is done, and that the result, if any, is available.

The fetch() function retrieves data. It's a global method on the window object. That means you can simply use it with fetch() in DevTools. The fetch function uses the following parttern: 

```
fetch("string representing a URL to a data source") 
.then(function(response) {
  return response.json();
}) .then(function(json){
  // Use this data inside of `json` to do DOM manipulation
}) 
```

the fetch function is provided a string representing a URL to a data source that stores its data in JSON. once a successful netwok call to the URL is completed, the  .then () method is called on the returned object. the then() take as its arguments a function that receives the reponse. he response has some basic functions on it for the most common data types. The most important ones are `.json()` and `.text()`.
```
.then(response => response.json())
```
The function above returns the content from the response. We can use that content inside of the callback function that's  passed in to the then() function below.
```
.then(response =>  { manipulate the DOM})
```
fetch can also add a  chaining method to respond to failed network call events. 
```
.catch(function(error) {
            alert("Please ensure all the fields are completed to reserve your restaurant");
        })
```

here is a complete example of an Asynchronous fetch request. 
```
fetch("https://api.documenu.com/v2/restaurant/")
.then(response => response.json())
.then(response =>  { manipulate the DOM})
.catch(function(error) {
            alert("Please ensure all the fields are completed to reserve your restaurant");
        })
```