# Why Elm?

In this section, we'll talk about the advantages — and disadvantages! — of using Elm to make front-end applications.


## First off, what is Elm?

**Elm is a language for building complex web interfaces.** Much like CoffeeScript or JSX, Elm compiles to JavaScript; the Elm Platform takes your Elm code and turns it into JavaScript that any web browser can understand. In many ways, it operates similarly to front-end JavaScript frameworks like React, Angular, and Ember.

Elm is more powerful than a frontend framework though: **it is a distinct programming language that can strictly enforce its opinions.**

You may have heard words like **functional** and **statically typed** used to describe Elm. **Functional** means that a function always returns the same value for a given input. **Statically typed** means that the compiler checks that the code makes sense before you can use it in production: it won't let you ask for the length of an integer or try to multiply a string and a float. If your code compiles, that means that you're doing operations that make sense. If you give a function the wrong *type* of value (a `String` rather than an `Int`) the Elm compiler will figure it out immediately and give you a hint.


## So why Elm?

One compelling reason is that **entire categories of bugs are impossible in Elm**, like:
  - "I expected this function to return a number, but it returned nil instead."
  - "Sometimes when I call this function it fails, even though I gave it the exact same input."
  - "Something is changing the value of my variable, and I'm not sure where it's happening."

These errors cannot happen in Elm because of the language's strictness. Indeed, the rules mean that **Elm applications can never accidentally crash.** There are no runtime exceptions — no `undefined is not a function` or `undefined method for nil:NilClass`. Consequently, Elm developers spend much less time in the Developer Tools console than JavaScript developers, and less time in the browser in general.

Because Elm requires all programs to follow its rules, **the Elm compiler will tell you exactly what's wrong with your program if you make a mistake**. It will tell you if you made an `if/else` expression return two different kinds of values, if you are calling a function with too many arguments, or if you are referencing a variable that does not exist.

Developing with Elm often feels like an ongoing conversation with the compiler, gently pushing you toward writing better code. Often, you don't even need to look at your application in the browser while implementing a feature — you can trust the compiler to tell you if you are going in the right direction.


## Why not Elm?

If you are coming from an object-oriented, dynamically typed language like Ruby or JavaScript, Elm can feel like a straightjacket. There are no `each` or `for` loops in Elm — instead, you use functions like `map`, `filter`, and `fold`. If you need to change a value deep inside a nested data structure, you can't simply read the value and mutate it, as you could in other languages.

Working with widget libraries can be hard due to conflicting paradigms. If you need to use [D3.js](https://d3js.org/) or [Three.js](https://threejs.org/), you may have difficulties using Elm.

## Learning Elm

You may be asking yourself why you should choose to learn a language that's so different from other tools in the ecosystem--especially if you aren't looking to work with it professionally yet. **We'd argue that the experience of working in an alien environment, even if it's just for a little while, can be fruitful.** You are probably not used to dealing with the constraints of purity, immutability, and static typing, which together make up the basic tenets of **functional programming**. These constraints will push you to solve problems in creative ways, and hopefully you will learn strategies that you can employ in other languages.

We make no claim that functional programming is *better* than other types of programming, but it definitely is *different*. We strongly believe that learning a new way to think about programming will make you a better developer, in the same way that learning a foreign language makes you appreciate the architecture and beauty of the languages you already know.

So let's get started!
