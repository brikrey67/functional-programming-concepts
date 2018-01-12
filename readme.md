# Concepts of Functional Programming

## Learning Objectives

- Explain the ideas of programming paradigms and design patterns
- Write pure functions
- Define the concepts of state and immutability
- Highlight advantages of functional programming
- Utilize a function closure to encapsulate data 

## Framing (15 minutes)

This lesson presents a high-level overview of fundamental concepts from functional programming and how they relate to 'modern' JavaScript. The goal of this lesson isn't to teach you how to write in a completely pure, functional style in JavaScript, but to explore the influence of these concepts in the current landscape of JavaScript development. It's also going to provide us with an additional different lens to examine *how we write, think about, and design our code*, allowing us to understand JavaScript a little more deeply.

Programming at its most basic level is the process developers undertake to instruct a computer to perform a task. Our thinking takes on very specific patterns as we learn to solve problems using code that reflects a patterned and logical approach to solving a given problem, whether that problem be an algorithm-based code challenge or providing a user interface that delivers a remarkable user experience (UX).

On an even higher or more abstract level, we are also writing our code according to rules and features of JavaScript itself. Possibly without even knowing it, we've been writing JavaScript according to a certain **programming paradigm**. 

So far, we dipped our toes into the **object-oriented paradigm**. We constantly interact with different kinds of objects all the time in JavaScript: Arrays `[]`, Objects `{}`, the `document` (the DOM, or Document *Object* Model), npm dependencies brought into our node programs with `require()`, `jQuery`, and so on.

The **OOP** paradigm also allows us to considerably DRY up our code to achieve ***abstraction*** (a constructor function that we can invoke to produce Objects), ***encapsulation*** (related data packaged in instances of objects), and ***modularity*** (reusable modules of code, often ones that work well with specific other modules of code). We can use ES2015 classes (or just plain old pre-ES6 constructor functions) to churn out different kinds of objects. Let's look at an example where the kind of Object will be a `Car`...

```js
//ES5-style constructor function for a Car (this is essentially what an ES6 class is)
function Car (make, model) {
  this.make = make
  this.model = model
  this.fuel = 100
  this.miles = 0
  this.drive = function () {
    this.fuel--
    return ++this.miles
  }
}

//ES6+
class Car {
  constructor (make, model) {
    this.make = make
    this.model = model
    this.fuel = 100
    this.miles = 0
  }

  drive () {
    this.fuel--
    return ++this.miles
  }
}
```

Each **programming paradigm** has its own **design patterns**. **Design patterns** categories of solutions to problems that the design of a programming language always faces...

> A couple design patterns, briefly...

| Question        | Answer          |
|-------------------|--------------------|
|How should data be encapsulated? | In an Object.|
|With an object, how will data be read/written? | Using **setter and getter** methods defined on the Object|
| What If I want to be 'passively' informed of changes to data, rather then having to 'get' the data all the time? | **subscribe and publish** methods |

However, in JavaScript, we can achieve this same ***abstraction***, ***encapsulation***, and ***modularity*** by using functions in ways that draw from the **functional programming paradigm**.



### Shared State

Think about the methods on an an instance of a `Car` from the example earlier...

> Copy and paste the code below into your browser console or other REPL.

```js
//ES5 style...
function Car (make, model) {
  this.make = make
  this.model = model
  this.fuel = 100
  this.miles = 0
  this.drive = function () {
    this.fuel--
    return ++this.miles
  }
}

let geoMetro = new Car('Geo', 'Metro')

geoMetro.drive()
```

On the `Car` instance named `geoMetro`, there is what we call **state**, which refers to the specific values at a given moment...

```
Car { make: 'Geo', model: 'Metro', fuel: 99, miles: 1 }
```


### Closures as an Alternative to Objects

With object-oriented programming we have **stateful** objects that encapsulate our data. However, in functional programming, we would represent the same data in functions instead of objects. By avoiding stateful objects, each with an individual state, we could pass this data into functions as arguments. With this approach, we are opting for calculation or evaluation over having an object with a state.

```js
//object-oriented approach
class Sum {
  constructor (initialValue) {
    this.value = initialValue
  }

  addToTotal (valueToAdd) {
    this.initialValue += valueToAdd
  }
}

//functional approach 
// https://en.wikipedia.org/wiki/Function_object#In_JavaScript
function Sum (initialValue) {
  const current = initialValue;
  return function (valueToAdd) {
    return current += valueToAdd
  }
}
```


JavaScript from the very beginning has had some functional tendencies. Brendan Eich originally envisioned the browser's having [an implementation of the functional programming language named 'Scheme' for the browser](https://auth0.com/blog/a-brief-history-of-javascript/). In other words, JavaScript, before it took shape and was named, was supposed to be a functional programming language. JavaScript as we know it ended up taking a different trajectory, but ultimately emerged as a language with some features of a functional language, primarily that *functions can referenced and passed as a value*, just as you would a number, string, null, NaN, undefined, Array, Object.

> Oddly enough, functions are actually objects in JavaScript. They are special in that they can be *invoked* or called `()`. 

Some of the concepts from functional programming have become important in modern JavaScript development. Ultimately, JavaScript, while having some tendencies of a functional programming language, wasn't designed as a functional programming language and has limitations in how well or how fully it can implement the functional paradigm.

## Why Functional Programming? (5 minutes)

Functional programming is a [hot and trendy topic](https://www.smashingmagazine.com/2014/07/dont-be-scared-of-functional-programming/) in web development right now, but it's far from being a new concept. LISP, one of the first programming languages ever created -- back in the 1950s -- had already embraced the paradigm, and has its foundations in [Alonzo Church](https://en.wikipedia.org/wiki/Alonzo_Church)'s work in [lambda calculus](https://en.wikipedia.org/wiki/Lambda_calculus) in 1930s, which very strongly influenced the development of LISP.

[Ardent fans](https://www.youtube.com/watch?v=BMUiFMZr7vk&t=1s) have lauded functional programming for its emphasis on writing programs that will result in fewer bugs and more reusable code. Programs that are 'composed' in this way are built out of small, highly-predictable functions with reliable behavior, that are well suited for being building-blocks for a stable code base.

The functional paradigm has historically been used with large-scale systems spanning thousands of networked computers, where it's critical that the program do exactly what's expected every time in the interest of performance and integrity. 

Many shied away from it, however, because "pure" functional languages are challenging to grasp and the paradigm was perceived as too "computer science-y" and academic. Functional programming does indeed have a daunting learning curve and a lot of terminology, but it is more accessible today than ever.

***So why is functional programming seeing a resurgence?***

[JavaScript is cool now](http://blog.salsitasoft.com/why-now/) and more developers than ever are writing JavaScript. As a result, JavaScript has been influenced by other languages indirectly though on a large scale, with each JavaScript developer. JavaScript's recent functional influences come from functional programming languages like LISP, Haskell, and Clojure. 

JavaScript technologies like Lodash, Immutable.js, React, and Redux make extensive use of core concepts of functional programming. The power of these technologies come from how each implements these concepts. In the scope of this course, we're concerned in particular with React, and later Redux, and how fundamental functional programming concepts apply to working with these 2 technologies.


## What is Functional Programming? (15 minutes)

Functional programming is characterized by **pure functions** that by definition that avoid...
  * side-effects
  * state or shared state
  * mutating data
  * changing values outside of their scope

### Pure Functions

Pure functions are a fundamental part of functional programming.

When we say **pure** we mean a function, ***given the same inputs, will always return the same output***. 

```js
const add = (addend, augend) => addend + augend

add(1,3) // this will always return 4 no matter what.
```

Such a function **does not** rely on or modify **state** outside its scope. Instead of sharing a parent state (in the form of a instance property on an object, or in the form of a global variable), the functional programming paradigm has functions pass around state (the data inside your application) via parameters, the input(s) to function, and `return` statements, or in other words, the output of the function. It's a bunch of functions passing data around, and a different way of organizing code than we've seen.


### Impure Functions

> Pure functions don't talk to strangers (no outside variables).

The execution of a pure function doesn't depend on the state of the system. It doesn't talk to global variables. It only deals with its input, and provides the same output for that specific input every time. 

Programs composed of pure functions avoid **shared state** and **tight coupling** between parts of an application. 

In practice, when using pure functions to pass around data, or the state of the application, they should be independent of one another, but work together. How does this work? Each function will have a very specific task which provides part of a larger solution. In many situations, you could think of each function as being a step in a list of instructions for solving a problem. Larger programs are built from **composing** each of these functions into larger, **higher-order functions**.

* What's an example of a side-effect we've commonly seen?

Here's an example of an impure function...

```js
let age = 27
function increaseAgeBy(int) {
  return age += int
}
increaseAgeBy(2)
```

<details>
  <summary>
    What makes this function impure?</summary>
  <p>
    The function changes variables outside of the function. This is a side-effect of the calling the function.
  </p>
</details>

<details>
  <summary>
    How can you demonstrate the impurity?
  </summary>
  <pre>
    console.log(age)
  </pre>
</details>

##### Refactor the Impure

We can make this function pure by not changing anything outside the function. Instead, we modify the parameter, which is in the scope of the function.

```js
let age = 27

function increaseAgeBy(myAge, int) {
  return myAge += int
}

increaseAgeBy(age, 2)
```

<details>
  <summary>How can you demonstrate the purity?</summary>
  <code>console.log(age)</code>
</details>

#### Pure or Impure?

> 5 min exercise, 10 min review.

For the following examples, pair with a partner and consider whether or not each function is a pure function. Is the function going to return the same thing every time for a given input? Is it changing things outside of its scope?

Test the following functions out in your browser console using the code snippets below...

```js
//A
const makeDoctor = (fullName) => `Dr. ${fullName}`

//B
function showSum (addend, augend) {
  console.log(addend + augend)
}

//C
const title = 'Dr. '
function makeDoctor (fullName) {
  return title + fullName
}

//D
const getRandom = (min, max) =>{
  const distance = max - min
  const upperBound = distance + 1
  return Math.floor(Math.random() * upperBound + min)
}

//E
function clearCounter () {
  counter = 0
}

//F
const axios = require('axios')

function getData (url) {
  return axios.get(url)
              .then(results => results)
}

//G
function deleteFrom (array, index) {
  array.splice(index, 1)
  return array
}

// test the function above (G) with the lines below... 
// const nums = [1, 2, 3, 4, 5, 6, 7]
// deleteFrom(nums, 2)
// console.log(nums)

//H

//How many side-effects are occurring here?
const mongoose = require('mongoose')
const Taco = require('../models/taco.js')

function getAllTacos (request, response) {
  Taco.find({})
      .then(results => response.json(results))
}
```

#### Views as Pure Functions in React

We haven't learned much about React, perhaps the most popular views library (the V in MVC), but one fundamental idea in React is applying the concept of pure functions to views the user interface. The manner in which React renders views roughly follows this pattern, we pass in inputs into a React component and get a part of a view.

<!-- TODO: refine phrasing above -->

We don't live in a black-and-white world, and functional programming is well-suited some things, and object-oriented for others. Approaches can be combined, or used to address specific problems.

### Functional Programming and the DOM

The value of a pure function is evident with views: a JavaScript function will construct a view by building parts of a view from some input, and create the *the exact same view from that input every time*. This adds a good deal of predictability to how our views are created in our applications. 

In a strict sense, the examples below contain side-effects, mainly the interaction with the DOM. There are times when JavaScript developers must write functions with side effects. Examples also include interactions with servers and databases. We are compromising the purity of these functions since we are introducing side effects, but only out absolute necessity.

In one sense, we have compromised the purity of the functions, but the aim of doing functional programmer developing web applications should be to keep functions as close to pure as possible and **only involve side effects when absolutely necessary**.

Note also that each function has one, specific purpose. The functions are individually designed to handle one task and do not depend on one another in order to execute. While that is true, these functions are designed to work together and their purposes are linked.

```js
// "The call is coming from inside the function!"

document.body.appendChild(
  ul( // 3 arguments are being passed to the function ul, 
    li( // the returns of 3 calls to li
      a('Home', '/') // each li receives the return of a call to `a` as an argument
    ),
    li( 
      a('About', '/about') 
    ),
    li( 
      a('Contact Us', '/contact') 
    )
  )
)

// ES6 rest parameter, from MDN: "The rest parameter syntax allows us 
// to represent an indefinite number of arguments as [a single] array."
// However many arguments are passed to ul, they be captured in a
// single array, listItems.
function ul (...listItems) { 
  console.log(listItems) // STRANGER DANGER / Side-effect Alert: logging to the console  
  const unorderedListElement = document.createElement('ul')

//appends all the <li>s to the <ul>
  return listItems.reduce((accumulatedListItems, listItem) => { 
    accumulatedListItems.appendChild(listItem)
    return accumulatedListItems
  }, unorderedListElement)
}

function li (childElement) {
  const baseElement = document.createElement('li')
  baseElement.appendChild(childElement)
  return baseElement
}

function a (text, href) {
  const anchor = document.createElement('a')
  anchor.innerHTML = text
  anchor.href = href
  return anchor
}
```

We've gotten a glimpse of how to structure a small piece of a program with functions that work together, albeit in a fairly simplistic way. There are many ways to use functions together, especially with complex high-order functions. Within functional programming higher-order functions is an extremely rich category of increasingly complex functions.

With a lot of functions passing around data, tight control over how that data is pass becomes critical. This ties into the importance of one-way or immutable data flow in functional programming. 


## Immutable Data Flow

Simply put, it's the practice of not changing data being accessed in the function. Think back to the splice example.

```js
function deleteFrom (array, index) {
  array.splice(index, 1)
  return array
}

// test the function above with the lines below... 
// const nums = [1, 2, 3, 4, 5, 6, 7]
// deleteFrom(nums, 2)
// console.log(nums)
```

Since `.splice()` is a **mutator method**, it modified the state of the array it was called upon. How would we deal with that?

```js
// .slice() is nice... for copying arrays
function deleteFrom (array, index) {
  //   .splice() P_ermanently changes

  //   .slice() first, then
  //           .splice() 
  array.slice().splice(index, 1)
  return array
}

// new function same test
// const nums = [1, 2, 3, 4, 5, 6, 7]
// deleteFrom(nums, 2)
// console.log(nums)
```

If we can't change a value, then our approach to copy it, and then modify the copy. We now have some intuitive basis now to see why immutability might be important as a concept. It's simply the idea of *not changing data*, and instead *copying that data, and then applying a change to the copy of that data*.

When writing **pure functions**, it is important to completely avoid changing (or mutating) objects outside of the function, since that mutation would be a side-effect. This grants you greater certainty about what your code is doing, by ruling out side-effect shenanigans. Ultimately, embracing this limitation of writing as many pure functions as possible grants you the most control over how data flows.

Having pointed that out, let's look at where we run into this problem.

### Data Storage in Memory

Take a moment to enter in the follow code in your browser console...

```js
  let rabbitCount = 9000
  let rabbitCensus = rabbitCount
  rabbitCensus += 200 //short for rabbitCensus = rabbitCensus + 200

  //will rabbitCount change with the line above, or will rabbitCensus just change?
  console.log(rabbitCount)
  console.log(rabbitCensus)
```


```js
  let cats = ["Meowy Mandel", "Peter Criss", "Lion-O", "Cheetara"]
  let copyCats = cats

  copyCats.push("Garfield")

  console.log(cats)
  console.log(copyCats)
```

1. What happened here? is `copyCats` an independent copy of `cats`?
2. Why didn't this happen in the first example?
3. What might this suggest about how **different types** are stored in memory?

```js
  let spartacus = {
    isSpartacus: true
  }

  let noImSpartacus = spartacus

  spartacus.isSpartacus = false

  console.log(spartacus)
  console.log(noImSpartacus)
```


Immutable data flow may seem like an awkward limitation at first since it requires a different way of thinking about and dealing with data. Think about the concept of an undo history: we **really rely** on having an accurate history of the commands we've entered and actions we've taken in a program. If you were coding a feature like an undo history, you'd want to make sure that you had. Immutable data flow would be welcomed limitation in that sense. 

Why does the example below violate this concept of Immutability?

```js
let teenAndy = {
  name: 'Andy',
  age: 13
}

teenAndy.age = 20 // he's growing up so fast 😭
```

#### Copying Objects

If we wanted to make this change ***immutably***, we could create a function that would return a **new** and **separate** version of `instructor` without modifying `instructor` directly:

```js
let teenAndy = {
  name: 'Andy',
  age: 13
}

function updateAge (instructor, newAge) {
  let newInstructor = Object.assign({}, instructor)
  newInstructor.age = newAge
  return newInstructor
}

let currentAndy = updateAge(teenAndy, "Andy")
```
> Object.assign() is the simplest way to make a copy of an existing object

This example does not violate immutability because the original object (`instructor`) is not directly mutated. Instead, a copy of that object is created, then mutated, and finally returned. This way, the original object `instructor` is still accessible with its original values.


### Techniques for Dealing with Immutable Data

#### Mutator Methods

A **mutator method** is a method which *changes the thing (an array in this case) it is called upon*.

[Splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

`.splice()` ***is a mutator method***, meaning it modifies whatever it is called on.

[Slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) does not change what it is called upon and instead creates a copy.

`.slice()` ***is not a mutator method***. Use it for ***copying*** all or part of an array!

<details>
  <code>
    It's easy to confuse slice and splice, 
    so here is a mnemonic device.
  </code>
  <summary>
    <p> S<em><strong>p</strong></em>lice <em><strong>p</em></strong>ermanently mutates. </p>
    <p> S<em><strong>l</strong></em>ice <em><strong>l</em></strong>eaves the original alone. </p> 
  </summary>
</details>

#### Copying arrays of objects

For arrays of objects, you can use `map()` in concert with `Object.assign()`...

```js
let todos = [
  { 
    todo: "learn functional programming" 
  }, { 
    todo: "learn about currying and partial-application" 
  }, { 
    todo: "learn about thunks" 
  }, { 
    todo: "what's a monad tho"
  }, { 
    todo: "prevent head from exploding"
  }
]

let todosCopy = todos.map(obj => Object.assign({}, obj))
```

> Other noteworthy mutator methods are `.reverse()`, `.sort()`, `.pop()`, `.push()`, `.shift()`, and `.unshift()`.

You can also 'deep copy' objects with...

```js
function deepCopy (someObject) {
  return JSON.parse(JSON.stringify(someObject))
}

//copying objects like this is tricky
let deepObject = {
  subObject: {
    subSubObject: {
      finallyThereIsAProperty: true,
      butOhNoTheresAnArray: [{oh: 'nooo'}, {why: 'oh why'}, {mustThisObject: 'be'}, {so: 'complicated'}]
    }
  }
}

deepCopy(deepObject)
```

<!-- TODO: Deep Copy objects. -->

<!-- Thunks? -->
<!-- 
### Returning Functions from Functions

We can also build functions with other functions.

```js
function multiplyBy (num) {
  return (anotherNum) => num * anotherNum
}

const multiplyBy2 = multiplyBy(2)
const multiplyBy5 = multiplyBy(5)

console.log(multiplyBy2(4))
console.log(multiplyBy5(4))
``` -->

## Closures, a closing example

Notice that even though `content` in not defined within the function being returned, it is still remembered by the function through what is called the function's **closure**.

We can right some really neat code taking advantage of **closures**.

```js
function Locker (password) {
  let locked = true
  let content

  return {
    toggle (pwd) {
      if (pwd === password) {
        locked = !locked
      }
      return locked
    },
    read () {
      if (locked) {
        return "unlock to read"
      } else {
        return content
      }
    },
    write (newContent) {
      if (locked) {
        return "unlock to write"
      } else {
        content = newContent
        return content
      }
    }
  }
}
```

Eloquent JavaScript has a really great [explanation of closures](http://eloquentjavascript.net/03_functions.html#h_hOd+yVxaku).


### Review and Questions (10 minutes / 2:30)

- Check out the [Coding Meetup Kata's](http://www.codewars.com/kata/coding-meetup-number-1-higher-order-functions-series-count-the-number-of-javascript-developers-coming-from-europe) for lots more practice
- [Node School Workshoppers](https://nodeschool.io/#workshoppers)
- [Eloquent JS Higher-Order Functions](http://eloquentjavascript.net/05_higher_order.html)


## Additional Resources
  - https://github.com/getify/Functional-Light-JS
  - http://eloquentjavascript.net/1st_edition/chapter6.html
