#ES6

## Learning Objectives

- Explain the history of ES and JS
- Compare/contrast features of ES5 and ES6
- Explain when to use `var` vs `let` vs `const`
- Use template literals to interpolate variables and strings
- Use deconstruction to extract values from objects and arrays
- Use default parameters and arrow functions

## Framing

Today, we are going to be looking at a new way to write Javascript by playing with some of the new features released in ES6.

#### JS vs ES

As mentioned previously, JavaScript standard is officially referred to as [ECMAScript](https://en.wikipedia.org/wiki/ECMAScript).

As JS is so widely used, there is a body known as [TC39](https://www.ecma-international.org/memento/TC39.htm) or [ECMA International](https://www.ecma-international.org/), which formally approves official versions for release.

Each version contains features/changes to be added to the language.

In short, I like to think of ECMAScript as the language, and JavaScript as an implementation of that language.

#### Evolution of JS

> Check out [this awesome visualization](http://shaunlebron.github.io/solar-system-of-js/#0) of the current state of the JS universe

Condensed timeline:

- 1999 - ES3 was released, the first widespread use of the language.
- ES4 was never released, largely due to  political reasons.
- 2009 - ES5 was released, what we have been writing so far in class.
- 2015 - ES6 was published, releasing a wide set of new features and syntax.

#### Why now?

Many plugins, frameworks and modules still use ES5, as browser support for
the new version of the language is [still not universal](http://caniuse.com/#search=es6), but the new syntax and features
of ES6 are increasingly becoming more and more popular among many open-source projects and in the developing world at large. Also, you are very likely to see it pop up in the documentation of some of the technologies we will be using in this course.

Today is all about exploring some of the [new features](https://github.com/lukehoban/es6features) and getting comfortable with
the new syntax.

> For more backstory, we recommend checking out [this talk](https://www.youtube.com/watch?v=PlmsweSNhTw) from Brendan Eich on what he views as the future of JS.

<br />

## You Do
Take 20 minutes to read through this article: [Getting Started with ECMAScript 6](http://blog.teamtreehouse.com/get-started-ecmascript-6) from the Treehouse blog.  If you have time leftover, you can read about the differences between [Understanding ES5, ES2015 and TypeScript](https://johnpapa.net/es5-es2015-typescript/).

Also- enable experimental JS in Chrome [Chrome Flags](chrome://flags)

## New Features

### Block Scope

<details>
<summary>What does the concept of scope refer to in JS?</summary>

In short, the notion of which variables are available where.

</details>

---

<details>
<summary>So far in class, what is the primary way to control scope in JS?</summary>

If you wanted block level scope in ES5, you would need to use functions- either a regular function or an IIFE.

</details>

#### `let`

Functions in ES5:

```js
// es5
var a = 1;
function myFunction() {
  a = 2;
  console.log(a);
}
console.log(a);
myFunction();

// will print out 1, 2
```

ES6 introduces the concept of block scoping, which allows us to limit the scope of a variable declared with `let` to a given block `{ ... }`. It also avoids variables hoisting, as a variable is only declared/assigned where it exists within our code.

```js
// es6
var a = 1;
{
  let a = 2;
  console.log(a);
}
console.log(a);
// will print out 2, 1
```

You are more likely to see `let` declarations inside an `if` or `for` block because of the block scoping capability:

```js
// es5
for(var i = 0; i < 10; i++){
  console.log(i);
}
console.log("outside loop:", i);
// still have access to i outside of the loop

// versus

// es6
for(let j = 0; j < 10; j++){
  console.log(j);
}
console.log("outside loop:", j);
// throws an error
// because of block scope, j will not be available outside of the for block
```
#### `const`

ES6 introduces another keyword for declaring variables: `const`

In ES5, if you want to declare a variable that will remain constant, it is a common practice to write the name in all uppercase letters.  However, this will not prevent the variable from being reassigned, but it is more of a note to other developers about your intention.

`const` is an identifier for variables that will not be reassigned/read only variables:
  - not a constant variable, but a constant reference

```js
const a = 1;
a = 2;
// Throws an error in chrome

const a = 2;
// throws an error

var a = 2;
// throws an error
```

### Default parameters

With ES6, we now have the option to set default values for any of our functions' parameters.

```ES5
function hello(name){
    name = name || "Frankie P";
    console.log("Hello, " + name);
}

hello(); // Hello, stranger
hello("Jesse"); // Hello, Jesse

```ES6
function hello(name = "stranger"){
    console.log("Hello, " + name);
}

hello(); // Hello, stranger
hello("Jesse"); // Hello, Jesse
```

The ES6 way is generally better because you won't have 'or' expressions all over your code.

### Destructuring

The destructuring assignment makes it possible to extract data from complex data
types (arrays and objects) into distinct variables:

```js
let [a, b] = [1, 2];
// What is on the left looks like an array literal, but you are actually working with individual variables, and surrounding them with square brackets because you are destructuring an array. You are telling the first value in the array to assign itself to 'a', and the second value to assign itself to 'b'.
a; //= 1
b; //= 2
let nums = [1, 2, 3, 4, 5];
let [first, second, third] = nums;
first; //= 1
second; //= 2
third; //= 3
```

This also applies to objects:

```js
var user = {
    id: 1,
    name: "Bob",
    age: 43 ,
    profile_url:  "http://api.co/users/1",
    location: "DC"
}

// ES5
function greetUser (user) {
    console.log("Hello " + user.name + ", how's the weather in " + user.location + "?");
}

// In ES6 this becomes:
function greetUser({ name, location })  {
    console.log("Hello " + name + ", how's the weather in " + location + "?");
}
// You would call both by using: greetUser(user);

// If you are destructuring an object, you would surround the desired variables with curly braces, which will make it look like you are creating an object literal, but you are really just building an assignment statement.  You will want to pick off specific properties in the object.

```

### Concise Object Properties and Methods

ES6 allows us to shorten method definitions from:

```js
var car = {
  drive: function(){
    console.log("vroom vroom");
  }
}
```

to

```js
let car = {
  drive() {
    console.log("vroom vroom");
  }
}
```

And for properties where the key is the same as the variable storing the value:

```js
// ES5
var x = 1;
var y = 2;

var obj = {x:x, y:y};
```

```js
// ES6
let x = 1;
let y = 2;

let obj = {x,y};
```

### Template Literals

Template literals can help you build the string values that you might want to assign to a variable.  

Here is how we previously used variables as placeholders in order to evaluate strings/concatenate variables with strings.
```js
// ES5
var name = "Inigo Montoya";
var killee = "father";
var prepareTo = "die";

console.log("Hello. My name is "+ name + ". You killed my " + killee +". Prepare to " + prepareTo + ".");
console.log("Hello.\n" + 
"My name is "+ name + ".\n" + 
"You killed my " + killee +".\n" + 
"Prepare to " + prepareTo + ".");
```

In ES6, we can interpolate variables using template literal syntax: '(`)' (backticks), and replace string concatenation code

```js
// ES6
let name = "Inigo Montoya";
let killee = "father";
let prepareTo = "die";

console.log(`Hello. My name is ${name}. You killed my ${killee}. Prepare to ${prepareTo}.`);
```

A template literal can also be on many lines. 

```js
// ES5
var name = "Inigo Montoya";
var killee = "father";
var prepareTo = "die";

console.log("Hello.\n" + 
"My name is "+ name + ".\n" + 
"You killed my " + killee +".\n" + 
"Prepare to " + prepareTo + ".");
```

```js
// ES6
let name = "Inigo Montoya";
let killee = "father";
let prepareTo = "die";

console.log(
  `
    Hello. 
    My name is ${name}. 
    You killed my ${killee}. 
    Prepare to ${prepareTo}.
  `
);
```

And it would still be valid.

### Arrow Functions

Arrow functions are a new shorthand syntax for defining anonymous functions.  It gets its name from the syntax `=>`, which in other languages, is knows as: the fat arrow, the rocket or the Lamda operator.

```js
// ES5
let foods = ["pizza", "mac n cheese", "lasagna"];
foods.forEach(function(food) {
    console.log("I love " + food);
});
```

```js
// ES6
let foods = ["pizza", "mac n cheese", "lasagna"];
foods.forEach((food) => {
  console.log(`I love ${food}`);
});
```
You could get access to each element in this array using a `for` loop.  However, the forEach() method is a method on an array that will iterate through the array.  You pass in a function to the forEach method, and tell it what you want to do with each item (via the param(food, in this case)) in the array.

```js
// ES5- with a for loop
let foods = ["pizza", "mac n cheese", "lasagna"];
for(var i = 0; i < foods.length; i++) {
    console.log("I love " + foods[i]);
}
```

Even more concise syntax:

```js
// ES6
let foods = ["pizza", "mac n cheese", "lasagna"];
foods.forEach(food => console.log(`I love ${food}`));
```

If there is more than one parameter in the function, wrap them in parens:

```js
let foods = ["pizza", "mac n cheese", "lasagna"];
foods.forEach((food, i) => console.log(`My #${i} favorite food is ${food}`));
```

Arrow functions also have the benefit of not changing the value of `this`.

Additionally, the `return` statement is not needed with single line arrow functions. There is an **implicit return**.

```js
//ES5
function subtract(x, y) { x + y; }
//undefined in console
```

```js
// ES6
let add = (x, y) => x + y;
add(2, 3); //5
```

If the function is multi-line, you will need to explicitly return:

```js
let add = (x, y) => {
  return x + y;
}
add(2, 3);
```

## Modern Browsers

Make sure that if you are using Chrome, you enable the experimental javascript flag by going to `chrome://flags`. And then relaunch Chrome.

## Legacy Browser Support

Support for ES2015 is growing! - https://kangax.github.io/compat-table/es6/

If you need to support a legacy browser, check out the following transpilers.  A transpiler will convert one language into another.  In this case, it will convert your ES6 code back into ES5.
- [Traceur](https://github.com/google/traceur-compiler/wiki/Getting-Started)
  - project ran by google, which takes ES6 code and compiles it to ES5.
  - it doesn't support all of ES6.
  - [Traceur repl](https://google.github.io/traceur-compiler/demo/repl.html#)
  - [Plnkr](https://plnkr.co/)
    - make sure to add the traceur from the search packages.
      - will add traceur.js and bootstrap.js
      - if you have an external js file, just make sure to add a type="module" to the tag
- [Babel](https://babeljs.io/)
- [Addy osmani ES6 Tools](https://github.com/addyosmani/es6-tools)

** You need to make sure that you are supporting the browsers that your users are using. **

<br />

## Bonus

### Spread operator

The spread operator `...` allows an expression to be expanded into multiple elements.

This is useful for separating an array into individual elements:

```js
var dimensions = [10, 5, 2];
var volume = function(height, width, length) {
  return height * width * length;
}
// ES5
volume(dimensions[0], dimensions[1], dimensions[2]);

// ES6
volume(...dimensions);
```

You can also add two arrays together. Without the spread operator, you would be adding they array of a into nums, instead of the two arrays being added seamlessly together.

```ES5
var a = [4, 5, 6];
var nums = [1, 2, 3, a, 7, 8, 9];

nums;
> [1, 2, 3, [4, 5, 6], 7, 8, 9]
```

```ES6
var a = [4, 5, 6];
var nums = [1, 2, 3, ...a, 7, 8, 9];

nums;
> [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

The spread operator also makes it very easy to create copies of an array in functions where mutation occurs:

```js
var days = ["monday","tuesday","wednesday","thursday","friday","saturday","sunday"];

function reversedDays(arr){
  return arr.reverse();
}
console.log(reversedDays(days));
// but now days is no longer in order
console.log(days);

// To deal with this, we can either:

// ES5
function reversedDays(arr){
  var newArray = [];
  for(let i = 0; i < arr.length; i++){
    newArray.push(arr[i]);
  }
  return newArray.reverse();
}
console.log(reversedDays(days));
console.log(days);

// or... (<- pun)

// ES6
function reversedDays(arr){
  return [...arr].reverse();
}
console.log(reversedDays(days));
console.log(days);
```

<br />

## Keep Going

There are a lot of features in ES6 that we have not covered:

- [Rest Parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)
- [Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
- [Classes](http://es6-features.org/#ClassDefinition)
- [Inheritance](http://es6-features.org/#ClassInheritance)

## Resources
- [Const](http://es6-features.org/#Constants)
- [Let](http://es6-features.org/#BlockScopedVariables)
- [Block Scope](https://www.sitepoint.com/joys-block-scoping-es6/)
- [Arrow Functions](http://es6-features.org/#ExpressionBodies)
- [Template Literals](http://es6-features.org/#StringInterpolation)
- [Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_template_literals)
- [Destructuring](http://es6-features.org/#ArrayMatching)
- [Destructuring](http://www.2ality.com/2015/01/es6-destructuring.html)
- [Property Shorthand](http://es6-features.org/#PropertyShorthand)

- [You Don't Know ES6](https://github.com/getify/You-Dont-Know-JS/tree/master/es6%20%26%20beyond)
- [More History](https://benmccormick.org/2015/09/14/es5-es6-es2016-es-next-whats-going-on-with-javascript-versioning/)
- [ES6 Compatibility](https://kangax.github.io/compat-table/es6/)
- [Can I Use](http://caniuse.com/)
