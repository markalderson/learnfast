# Learn JavaScript in 10 minutes

I lied. You can't learn JavaScript in 10 minutes. But if you're a smart guy, 10 minutes is enough to grasp the basics. If you have some kind of programming background, no matter how good, this tutorial will be a piece of cake. But if you're really new to programming, you have to be _very_ smart to understand it, and I think it's probably better if you go learn JavaScript somewhere else. If you decide to stay, know that it will be fun.

## The developer console

To better understand this tutorial, you'll want to execute some JS (JavaScript) code and see what happens. The easiest way to do this is to open the _developer console_ of your browser. I'm not telling how to do it. Just google it. If you can't do this by yourself, you probably should give up on programming.

## Variables

Like in most programming language, JS allows you to create _variables_ to store _values_. Each value belongs to a specific _data type_, the simplest ones being numbers and _strings_ (i.e. text). _Operators_ (like the `+` sum operator) lets you combine two values. Operators and parentheses allow you to write possibly complex _expressions_.

``` javascript
var one = 1;
var two = 2;
var three = one + two;
var first_name = "marco";
var last_name = "liceti";
var complex_expression = ( 2 + 10 ) - ( 7 - 5);
```

## Comments

You can insert _comments_ in your code to leave a message to other readers or even to yourself (you don't know how time can pass before you read that code again: a note can be useful to understand what you wanted to accomplish when you wrote that code).

The point with comments is that the JS interpreter ignores them. They are notes for human readers and don't affect the program's behaviour.

You can insert a comment with `//`. The text following the `//` will be the content of the comment. These kind of comments can span only a single line. For multi-line comments you have to wrap your comment's text between `/*` and `*/`.

In the next paraghraphs I'll use comments to explain what the code does.

``` javascript
/*
  This is a multi-line comment to
  explain that the following is
  the same as the previous example
  but with comments inside.
*/
var one = 1; // this variable holds the number 1
var three = one + two; // this variable holds the number 2
var first_name = "marco"; // this variable holds the string "marco"
var last_name = "liceti"; // this variable holds the string "liceti"
var complex_expression = ( 2 + 10 ) - ( 7 - 5); // this variable holds an expression which evaluates 10
```

## Control flow statements

Some times you may need to execute code based on a condition, for example show some message only if the user of your application is logged in. Like most other programming languages, JS accomplishes this through the `if` _statement_. You can also specify what to do if the condition isn't met.

``` javascript
var age = 27;
if (age > 18) {
  console.log("Fuck!");
} else {
  console.log("Heck!");
}
```

Other times you need to repeat a block of code a number of times, or until a certain condition is true. You can achieve this with `for` or `while` statements. The following example shows how to calculate the three-times table with `for`:

``` javascript
for (var i = 1; i <= 10; i++) {
  console.log(3 * i); // this will be repeated 10 times
}
```

**Note:** `i++` means "take the value of `i` and increment it by one".

You can do the same with `while`:

``` javascript
var i = 1;
while (i <= 10) {
  console.log(3 * i); // this will be repeated 10 times
  i++;
}
```

You can use `if` inside `for` or `while` and `for` or `while` inside `if`. Actually, you can mix and _nest_ them however you like. Programming is very much about correctly mixing these statements in order to match the expected behaviour for your program.

## Functions

What you learned so far allows you to write any kind of program, believe it. But good code needs _modularity_.

The easiest form of modularity in programs is provided by _functions_. A function is a piece of a program you give a name to, and that you can _invoke_ multiple times later on. This way, if you need to perform the same task you don't to wirite the same code over and over again in different spots of your program.

Here is a simple JS function:

``` javascript
function sayHi() {
  console.log("Hi");
}
for (var i = 1; i <= 10; i++) {
  sayHi(); // says "Hi" 10 times
}
```

The coolest feature of functions is that they can be _parameterized_.

``` javascript
function say(what, who) {
  console.log(what + " " + who);
}
say("Hi", "marco"); // says "Hi marco"
```

Functions were also used in old programming environments to expose advanced features like file or network access.

## Objects

Objects are special values used to store other values called _properties_. Here some examples:

``` javascript
var marco = {}; // I just created an object and stored in the "marco" variable
marco.name = "marco"; // now the "marco" object has a string property called "name" with value "marco"
marco.age = 27; // now the "marco" object has a numeric property called "age" with value 27
console.log(marco.age); // Outputs 27
```

You can write the previous example in other ways:

``` javascript
var marco = {};
marco["name"] = "marco";
marco["age"] = 27;
console.log(marco["age"]);
```

``` javascript
var marco = {
  name: "marco",
  age: 27
};
console.log(marco["age"]);
```

Object properties may also be functions. In that cases, they are called _methods_:

``` javascript
var marco = {
  name: "marco",
  age: 27,
  sayHi: function () {
    console.log("Hi");
  }
};
marco.sayHi(); // Says "Hi"
```

Object properties can be other objects. You can nest them however you like.

## Arrays

Arrays are collections of values:

``` javascript
var names = [ "al", "john", "jack" ];
console.log(names[0]); // Outputs "al"
console.log(names[1]); // Outputs "john"
console.log(names[2]); // Outputs "jack"
```

Arrays can store any kind of value:

``` javascript
var stuff = [ "foo", 3, {} ];
// stuff[0] is the string "foo"
// stuff[1] is the number 3
// stuff[2] is an empty object
```

Arrays can also store other arrays and they can be object properties. Mix this stuff however you like / need.

## What to do now

This tutorial is already over.

If you have programmed in other languages before, now you're probably ready to write some JS code and to continue to learn the details by yourself.

If this is your first experience with programming, you'll be both excited and confused. I advise you to _try_ to write some code. Have a playful attitude. Then read a book. If it's a JS book, this tutorial will allow you to read it with less fear.
