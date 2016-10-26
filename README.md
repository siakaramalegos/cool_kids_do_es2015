# Cool Kids Do ES2015
Cool features of ES2015 - part of my lightning talk for Viking Code School

**Contents**
- [`const` and `let`](#const-and-let)
- [Default Parameters](#default-parameters)
- [Object Destructuring in Parameters](#object-destructuring-in-parameters)
- [Template Strings](#template-strings)
- [Spread Operator](#spread-operator)
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

## Spread Operator


## Arrow Functions
“Doesn’t actually bind this”
