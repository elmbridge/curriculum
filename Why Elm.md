# Why Elm?

In this section, we'll talk about the advantages — and disadvantages! — of using Elm to make front-end applications.

First, the basics: **Elm is a language for building complex web interfaces.** It is a language that compiles to JavaScript — much like CoffeeScript or ES6 build tools, the Elm Platform takes your Elm code and turns it into JavaScript that any web browser can understand. In many ways, it operates similarly to front-end JavaScript frameworks like React, Angular, and Ember.

So why do developers go to the trouble of using a whole new language instead of using a JavaScript framework? Indeed, Elm shares many of its opinions about architecture and code quality with those tools. However, **Elm is different in one important way — because it is a distinct programming language and not simply a framework, Elm can strictly enforce its opinions.**

And the language has lots of rules! They are meant to push developers toward writing code that is easier to maintain and harder to break. For instance:

- **If a function in Elm is given an input, it always returns the same output.** There is no notion of instance variables or `this` in Elm — the only thing a function can do is read the values of its arguments and call out to other functions. This quality of the language is called **purity** — no matter what context, a function will do the same thing every time.

- **Variables, once defined, can never change.** It's not possible, for instance, for a function to accidentally change its inputs, or for something to become `undefined`. If you need to add an element to a list, there is no way to do so destructively — instead, you have to create a new list with all the elements you specify. Values like these are called **immutable**.

- **Everything in Elm has a *type*. Nothing can ever break that contract.** For instance, if you make a `length` function that takes a string and returns an integer, it is not possible for that function to return a float, another string, or a null value (in fact, there are no null values in the entire language). Those same constraints operate on everything in the language, including variables, functions, and complex data structures. That is why Elm is called a **statically typed** language.

Because of these rules, **entire categories of bugs are impossible in Elm**, like:
  - "I expected this function to return a number, but it returned nil instead."
  - "Sometimes when I call this function it fails, even though I gave it the exact same input."
  - "Something is changing the value of my variable, and I'm not sure where it's happening."

These errors cannot happen in Elm because of the language's strictness. Indeed, the rules mean that **Elm applications can never accidentally crash.** There are no runtime exceptions — no `undefined is not a function` or `undefined method for nil:NilClass`. Consequently, Elm developers spend much less time in the Developer Tools console than JavaScript developers, and less time in the browser in general.

That strictness can come with real downsides, though. If you are coming from an object-oriented, dynamically typed language like Ruby or JavaScript, Elm can feel like a straightjacket at first. There are no `each` or `for` loops in Elm — instead, you have to use higher-order functions like `map`, `filter`, and `fold`. The `+=` operator has no place in the language either, since it would mutate the variable on its left-hand side. If you need to change a value deep inside a nested data structure, you can't simply read the value and mutate it, as you could in other languages.

You may wonder how Elm developers can survive with all these restrictions. The strictness of the language opens up other doors, however. Because Elm requires all programs to follow its rules, **the Elm compiler will tell you exactly what's wrong with your program if you make a mistake**. It will tell you if you made an `if/else` statement return two different kinds of values, if you are calling a function with too many arguments, or if you are referencing a variable that does not exist.

Developing with Elm often feels like an ongoing conversation with the compiler, gently pushing you toward writing better code. Often, you don't even need to look at your application in the browser while implementing a feature — you can trust the compiler to tell you if you are going in the right direction.

You may be asking yourself why you should choose to learn a language that's so different from other tools in the ecosystem. **We'd argue that the experience of working in an alien environment, even if it's just for a little while, can be fruitful.** You are probably not used to dealing with the constraints of purity, immutability, and static typing, which together make up the basic tenets of **functional programming**. These constraints will push you to solve problems in creative ways, and hopefully you will learn strategies that you can employ in other languages.

We make no claim that functional programming is *better* than other types of programming, but it definitely is *different*. We strongly believe that learning a new way to think about programming will make you a better developer, in the same way that learning a foreign language makes you appreciate the architecture and beauty of the languages you already know.

So let's get started!
