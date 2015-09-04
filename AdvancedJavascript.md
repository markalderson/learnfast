# Advanced JavaScript

Let's cover a couple of topics necessary in order to move to actual web development.

## Functional scope

Object-oriented languages (e.g. Java) usually have _block scope_. A scope may be defined as a set of accessibile variables.
Block scope means that when you define a block, you're creating a new scope. But what are blocks?
Blocks are simply sequences of instructions inside braces. Thus, you define a block every time you write a control-flow
statement (`if`,`for`, `while`) or a `function`. Every variable declared inside a block is accessible within that
block. Also, since blocks are nestable, scopes are nestable too. Each scope has access to variables
declared inside the enclosing scope. In other words, if a block A contains a block B, variables
declared inside A are accessible inside B. The converse is not true: variables inside B are not accessible inside A.
More specifically, variables declared inside a block are not accessible from the enclosing scope.

JavaScript has _functional scope_. This means that scopes are created only when you define a function. Variables
declared inside a function are accessible everywhere inside that function. Thus, variables declared inside a block
may be accessed also from the enclosing block. That's a JavaScript feature that confuses many developers coming
from other languages. The following example is valid JavaScript, while it would trigger an error in other languages:

``` javascript
function f1() {
  if (2 > 1) {
    var a = 7; // a is declared inside this block...
  }
  console.log(a); // ...but is also accessible outside of it
}

f1(); // outputs 7
```

In JavaScript you can declare a function inside another function. Scoping rules dictates that a function
can access all the variables declared inside the enclosing function.

``` javascript
function f1() {
  var a = 7; // a is declared inside this function...
  function f2() {
    console.log(a); // ...but is accessible inside this one too
  }
  f2();
}

f1(); // outputs 7
```

## Functions as values

In JavaScript functions are _values_. This means that you can pass them as arguments to other
functions.

``` javascript
function sayHi() {
  console.log('Hi');
}

function doSomething(what) {
  what();
}

doSomething(sayHi); // outputs 'Hi'
```

Also, you can return a function from another function.

``` javascript
function say(message) {
  return function () {
    console.log(message);
  };
}

var say_hello = say('Hello');

say_hello(); // outputs 'Hello'
```

## Closures

When you define a function, it will mantain access to the scope in which it was defined, even if
the function corresponding to that scope has terminated its execution.

``` javascript
function counter() {
  var i = 0;
  return {
    currentValue: function () {
      return i;
    },
    increment: function () {
      i = i + 1;
    }
  };
}

var c1 = counter();
c1.currentValue(); // 0
c1.increment();
c1.currentValue(); // 1

var c2 = counter();
c2.currentValue(); // 0
```

When they say JavaScript has _closures_, they talk about this kind of behaviour.

## Callbacks and Asynchronous / non-blocking I/O

Software development is the art of designing how to split work across software modules (i.e. functions or objects).
When a module delegates some work to another one, two approaches may be followed:

* partial delagation: delegate and then do something with the result
* full delegation: delegate and tell what to do with the result

The latter, in JavaScript, is based on the ability to pass function as arguments to other
function. When used this way, functions are called _callbacks_.

Here is an example where `module2` delegates work to `module1` via callback:

``` javascript
// Module1
function module1(callback) {
  // Define module1 work
  function doModule1Work() {
    // module1 work
  };
  
  // Execute module1 work
  var result = doModule1Work();
  
  // Handle the result with a function
  // passed from anther module
  callback(result);
}

// Module 2
function module2() {
  // Module2 callback
  function module2_callback(result) {
    // do something with the result
    // coming from a delegated module
  }
  
  // Delegate work to module1
  // and tell it to handle the result
  // with module2_callback
  module1(module2_callback);
}
```

Callbacks are heavily used in _frameworks_ and in _asynchronous / non-blocking I/O_.

A framework is a sort of software template that works by itself and you just customize by
writing proper callbacks and passing them to the framework's modules. More generally,
frameworks are reusable software systems that you include in your application. _Libraries_
are another example of reusable software, but they are different from frameworks
because instead of a working template they just offer "tools" that you need to figure out how
to use in your application to make it work. They don't use callbacks and may be considered
less powerful but easier to get started with. Also, they put less constraints on your application architecture.

Regarding asynchronous / non-blocking I/O, it's an optimized model for input and output operations.
Non-blocking means that when you request an I/O operation your program doesn't wait for the data
to be read / written and instead goes on with the next instruction. Using a callback you can
tell the JavaScript environment (that is responsible for executing I/O operations in parallel
with your code) what to do when the requested operation is complete.

This model makes your code more complex, but it can provide benefits both in multi-thread environments
and in single-thread environments like web browsers or servers like [Node.js](https://nodejs.org/). But
this discussion is a bit off-topic for this tutorial.

**Note:** A concept somewhat related to callbacks and asynchronous I/O is _event-driven programming_. It's an approach
to software design in which the flow of execution is modeled in terms of _events_. Some parts of the program
will _trigger_ events, some other parts _handle_ events. Asynchronous I/O may be seen as an event-driven design
in which the events are the completion (or failure) of an I/O operations. Event handlers are implemented with callbacks.

## Promises

As I said, asynchronous I/O makes your code more complex. Why? Because I/O operations are often related
and callbacks are good for single, isolated operations but they're inadequate for non-trivial flows of
operations.

Imagine you're a developer of a Twitter-like service. You'll eventually write code that, given a tweet,
fetches data about the user that wrote it. Maybe, you also want the number of re-tweets. Here is some example code
you can write:

``` javascript
function tweetData(tweet, callback) {
	database.fetchUserByTweet(tweet, function (user) {
		database.fetchRetweetsOfTweet(tweet, function (retweets) {
			callback({
				text: tweet.text,
				username: user.username,
				num_retweets: retweets.length
			});
		});
	});	
}

tweetData(tweet, function (data) {
	console.log(data); // outputs data collected through multiple callbacks
});
```

What you just saw is an example of what JavaScript developers call _Pyramid of Doom_: a callback, inside
a call back, inside a callback, etc.. Closures makes this kind of code easier to write, but still it has
a few drawbacks.

Code based on _promises_ is often a better solution. A promise is an object representing a pending
operation. It has a `then` method that accepts a function that will perform some work on the
result of the pending operation, whenever it will become available. Also, `then` returns a new
promise whose result will be the one return by the function it is passed to.

If the `database` object used in the previous example had supported promises, we could have written:

``` javascript
function tweetData(tweet) {
	var username_promise = database.fetchUserByTweet(tweet).then(function (user) {
		return user.username;
	});
	var num_retweets_promise = database.fetchRetweetsOfTweet(tweet).then(function (retweets) {
		return retweets.length;
	});
	var promises = Promise.all([tweet.text, username_promise, num_retweets_promise]);
	return promises.then(function (result) {
		return {
			text: result[0],
			username: result[1],
			num_retweets: result[2]
		};
	});
}

tweetData(tweet).then(function (tweet_data) {
	console.log(tweet_data);
});
```

## Prototypal Inheritance
