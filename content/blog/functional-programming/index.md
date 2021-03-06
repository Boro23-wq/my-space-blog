---
title: Functional Programming
description: Composing pure functions, avoiding shared state, mutable data...
date: 2020-01-20
---

<ins class="sub-ins-2">Functional programming</ins> is composed of pure functions, avoiding shared state, mutable data, and side-effects. They are declarative rather than imperative, and application state flows through pure functions and they do not share and colocate with methods in objects.

But do we need to change the paradigm from OOP? The answer lies below:

> Functional code tends to be concise, more predictable, easier to test, reuse, and handles concurrecy more effectively than imperative code.

There are basically 5 Functional Programming Principles:

- <ins class="sub-ins-2">Purity</ins>
- <ins class="sub-ins-2">Higher-order functions</ins>
- <ins class="sub-ins-2">Immutability</ins>
- <ins class="sub-ins-2">Function Composition</ins>
- <ins class="sub-ins-2">Currying</ins>

Ok so what do they mean? Lets dive deeper, shall we?

## <ins class="sub-ins">Purity</ins>

A pure function is a function which returns the same output, given the same input. They act on their parameters and has no side effects. A pure function will look like the code below:

```javascript
function Pure(a, b) {
  return a + b
}
```

But how do unpure functions look? Well! have a look at the code below:

```javascript
function Pure(a, b) {
  return Date.now()
}
```

## <ins class="sub-ins">Immutability</ins>

There are no variables in Functional Programming. Everything is treated as a constant here. Do you know when do we mutate these variables?

- <ins class="sub-ins-2">Short living loop variables</ins>
- <ins class="sub-ins-2">Loop flow structures</ins>
- <ins class="sub-ins-2">State Objects</ins>

So why do we need them? Immutability is the central concept of functional programming because without it, the data flow in your program is lossy. Let us try that in code. Shall we?

```javascript
const a = Object.freeze({
  foo: "Hello",
  bar: "world",
  baz: "!",
})
a.foo = "Goodbye"
```

> //Error: Cannot assign to read only property 'foo' of object Object

## <ins class="sub-ins">Higher Order Functions</ins>

In functional programming a function is a first-class citizen, meaning a function is just another value. So what are they used for often? Lets dig in.

- Abstract or isolate actions, effects, or async flow control using callback functions, promises and so on.
- Partially create a curried function for the purpose of reuse,
- Grab a few functions and instead returns some kind of composition of those input functions together,

Lets take a look at a code to have a good idea what higher-order functions are.

```javascript
const double = n => n * 2
const doubleMap = numbers => numbers.map(double)
console.log(doubleMap([2, 3, 4])) // [ 4, 6, 8 ]
```

You see how Array.prototype.map() allows you to abstract the data type from the mapping utility to make map() usable with any data type. That is what a higher order function generally do.

## <ins class="sub-ins">Function Composition</ins>

Functional composition is basically applying one function to the result of another to produce a third function. Lets grab a code and have a good idea what composition functions are all about.

```javascript
const add10 = n => n + 10
const multiply5 = n => n * 5
const add5AndMultiply5 = val => multiply5(add10(val))
```

> A composition can be simply defined as: h = f(g(x))

## <ins class="sub-ins">Currying</ins>

A curried function only takes a single parameter at a time. It keeps returning a new function (that expects the current argument) until all the arguments are exhausted. The arguments are kept "alive" (via closure) and all are used in execution when the final function in the currying chain is returned and executed.

Let us understand currying using code:

```javascript
function multiply(a) {
  return b => {
    return c => {
      return a * b * c
    }
  }
}
log(multiply(1)(2)(3)) // 6
```

Here in the code we have turned the multiply(1,2,3) function call to multiply(1)(2)(3) multiple function calls. We can certainly seperate the multiply(1)(2)(3) to understand it better:

```javascript
const mul1 = multiply(1)
const mul2 = mul1(2)
const result = mul2(3)
```

> log(result); // 6

There we go! That is all about Functional Programming. Until next time.
