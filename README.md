# Cool Kids Do ES2015
Cool features of ES2015 - part of my lightning talk for Viking Code School

**Contents**
- [`const` and `let`](#const-and-let)
- [Default Parameters](#default-parameters)
- [Object Destructuring in Parameters](#object-destructuring-in-parameters)
- [Template Strings](#template-strings)
- [Rest and Spread](#rest-and-spread)
- [Arrow Functions](#arrow-functions)

## `const` and `let`
[MDN Docs for const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const), [MDN Docs for let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
Pink is the new black and `let` is the new `var`. `const` is for single-assignment, or read-only items - the name cannot be reassigned but you can, for example, add a new key-value pair to an object `const`. Use `const` unless you really need a reassignable variable - it makes for cleaner, easier to understand code.

What else is different? They are block-scoped (see more [here](https://babeljs.io/docs/learn-es2015/)). For example, they can be scoped to `if` and `for` blocks. This is especially cool for `let` as it starts to behave a little more predictably in situations like this where you might have inadvertently created a closure...

Given HTML:
```html
<div id="hi1">Hi #1!</div>
<div id="hi2">Hi #2!</div>
<div id="hi3">Hi #3!</div>
```

And JavaScript:
```javascript
for(let i = 1; i < 4; i++) {
  document.getElementById('hi' + i)
    .addEventListener('click', function() { console.log(i) })
}
```
If you replace the `let` with `var`, you would always get 4 logged to the console rather than the expected behavior of 3.

## Default Parameters
[MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)

The old way - we couldn't set a default value for the parameter passed to the function (we would have to check as a separate line inside the function):
```javascript
function greeting(name){return name}
greeting('sia')   //  'sia'
greeting()        //  undefined
```

The new way:
```javascript
function greeting(name='sia'){return name}
greeting('voldemort')   //  'voldemort'
greeting()              //  'sia'
```

## Object Destructuring in Parameters
[MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

First, what's object destructuring?
```javascript
var [a, b, c] = [1, 2, 3]
a  //  1
b  //  2
c  //  3

var {a, b, c} = {a: 1, b: 2, c: 3}
a  //  1
b  //  2
c  //  3
```

It's even cooler when you realize you can use it in parameters (among many other things):
```javascript
function greeting({language, name}) {
  if (language === 'Greek') {
    return `Geia sou ${name}!`
  } else {
    return `Hello ${name}`
  }
} 
var options = {language: 'Greek', name: 'Sia'}
greeting(options)  //  'Geia sou Sia!'
```
Wait, what's that back-tic stuff? Well...

## Template Strings
[MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)

It's like Ruby interpolation but in JavaScript!
(from Babel's [Learn ES2015](https://babeljs.io/docs/learn-es2015/))
```javascript
// Basic literal string creation
`This is a pretty little template string.`

// Multiline strings
`In ES5 this is
 not legal.`

// Interpolate variable bindings
var name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`
```

## Rest and Spread
[MDN Docs for spread](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator), [MDN Docs for rest](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)

(partially from Babel's [Learn ES2015](https://babeljs.io/docs/learn-es2015/))
Turn an array into consecutive arguments in a function call. Bind trailing parameters to an array using a rest parameter:
```javascript
function f(x, ...y) {
  // y is an Array
  return x * y.length;
}
f(3, "hello", true) == 6
```

The spread operator helps reduce boilerplate code for multiple arguments...
```javascript
function f(x, y, z) {
  return x + y + z;
}
// Pass each elem of array as argument
const args = [1,2,3]
f(...args) == 6
```

## Arrow Functions
[MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
Arrow functions help reduce boilerplate syntax and also share the same lexical `this` as their surrounding code.

Here's an example of shorter length/syntax:
```javascript
var a = [
  "Hydrogen",
  "Helium",
  "Lithium",
  "Beryl­lium"
];

var a2 = a.map(function(s){ return s.length });
var a3 = a.map( s => s.length );
```

Here's an example of sharing lexical `this`. This is what we had to do before arrow functions to get functions with different scopes to behave as expected inside objects:
```javascript
function Person() {
  var that = this;
  that.age = 0;

  setInterval(function growUp() {
    // The callback refers to the `that` variable of which
    // the value is the expected object.
    that.age++;
  }, 1000);
}
```

But arrow functions allow us to write much less code to get the results that we intend:
```javascript
function Person(){
  this.age = 0;

  setInterval(() => {
    this.age++; // |this| properly refers to the person object
  }, 1000);
}

var p = new Person();
```
