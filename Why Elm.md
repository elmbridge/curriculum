# Why Elm?

In this section, we'll talk about the advantages — and disadvantges! — of using elm to make front-end applications.

First, the basics: **Elm is a language for building complex web interfaces.** It is a language that compiles to JavaScript — much like CoffeeScript of ES6 build tools, the elm platform takes your elm code and turns it into JavaScript that your browser can understand. In many ways, it operates similarly to front-end frameworks like React, Angular, and Ember.

So why would developers choose to use this new tool, instead of a more mainstream tool? Indeed, Elm shares many of its opinions about architecture and code quality with the popular JS frameworks. However, **elm is distinct in one important way — because it is a distinct programming language, not simply a framework, it can strictly enforce it's opinions.**

And the language has lots of rules! They are meant to push developers toward writing code that is that easier to maintain and harder to break. For instance:

- **If a function in elm is given an input, it always returns the same output.** There is no notion of instance variables or `this` in elm — the only thing a function can do is read the values of its arguments and call out to other functions. This quality of the language is called **purity** — no matter what context, a function will do the same thing every time.

- **Variables, once defined, can never change.** It's not possible, for instance, for a function to accidentally change it's inputs, or for something to become `undefined`. If you need to add an element to a list, there is no way to do so destructively — instead, you have to create a new list with all the elements you speicify. Values like these are called **immutable**.

- **Everything in elm has a *type*. Nothing can ever break that contract.** For instance, if you make a `length` function that takes a string and returns an integer, it is not possible for that function to return a float, another string, or a null value (in fact, there are no null values in the entire language). Those same constraints operate on everything in the language, including variables, functions, and complex data structures. That is why elm is called a **statically typed** language.

Because of these rules, **entire categories of bugs are impossible in elm**, like:
  - "I expected this function to return a number, but it returned nil instead."
  - "Sometimes when I call this function it fails, even though I gave it the exact same input."
  - "Something is changing the value of my variable, and I'm not sure where it's happening."

These errors cannot happen in elm because of the language's strictness. Indeed, the rules mean that **elm applications can never accidentally crash.** There are no runtime exceptions — no `undefined is not function` or `undefined method for nil:NilClass`. Consequently, Elm developers spend much less time in the Developer Tools console than JavaScript developers, and less time in the browser in general.

That strictness can come with real downsides, though. If you are coming from an object oriented, dynamically typed language like Ruby or JavaScript, elm can feel like a straightjacket at first. There are no `each` or `for` loops in elm — instead, you have to use higher-order functions like `map` and `filter`. The `+=` operator has no place in the language either, since it would mutate the variable on it's left-hand side. There is no `debugger` or `binding.pry` — elm's strict ruleset makes building a runtime debugger impossible.

These tools are useful in other languages, and you may wonder how elm developers can survive without them. The strictness of the language opens up other doors, however. Because elm requires all programs to follow it's rules, **the elm compiler will tell you exactly what's wrong with your program if you make a mistake**. It will tell you if you made a `if/else` statement return two different kinds of values, or if you are calling a function with too many arguments, or if you are referencing a variable that does not exist.

Developing elm often feels like an ongoing conversation with a compiler, gently pushing you toward writing better code. Often times, you don't even need to look at your application in the browser while implementing a feature — you can trust the compiler to tell you if you are going in the right direction.

You may be asking yourself why you should choose to learn a language that's so different from other tools in the ecosystem. **We'd argue that the experience of working in an alien envrionment can be productive, even if it's just for a little while.**  You are probably not used to dealing with the constraints of purity, immutability, and static typing, which together make up the basic tenets of **functional programming**. These constraints will push you to solve problems in creative ways, and hopefully you will learn strategies that you can employ in other languages.

We make no claim that functional programming is *better* than other types of programming, but it definitely is *different*. We strongly believe that learning a new way to think about programming will make you a better developer, in the same way that learning a second language makes you appreciate the architecture and beauty of the languages you already know.

So let's get started!
