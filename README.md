# Cool Kids Do ES2015
Cool features of ES2015 - part of my lightning talk for Viking Code School

## Default Parameters
[MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)

The old way - we couldn't set a default value for the parameter passed to the function (we would have to check as a separate line inside the function):
```
function greeting(name){return name}
greeting('sia')   //  'sia'
greeting()        //  undefined
```

The new way:
```
function greeting(name='sia'){return name}
greeting('voldemort')   //  'voldemort'
greeting()              //  'sia'
```

## Object Destructuring in Parameters
[MDN Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

First, what's object destructuring?
```
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
```
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
```
// Basic literal string creation
`This is a pretty little template string.`

// Multiline strings
`In ES5 this is
 not legal.`

// Interpolate variable bindings
var name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`
```

