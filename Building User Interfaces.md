# Building User Interfaces

Congratulations on completing the last lesson! If this was your first experience with a functional programming language, it may have been difficult. The jump from object oriented programming to functional programming can be scary, and Elm's syntax can be confusing for recent transplants. **This initial struggle is totally normal**, and will eventually dissapate as you continue to work with the Elm.

As we discussed earlier, Elm is distinctive in it's enforcement of **purity**, **immutability** and **static typing**. That's all well and good for the toy problems that you just solved, but you may be wondering how Elm can model a complex, interactive UI given these constraints. If nothing can change in Elm, how can Elm applications model systems that change?

Built into the language, Elm has a series of abstractions that are helpful in modeling user interfaces. Together, these abstractions form **the Elm architecture**, which is a detailed template for constructing an application in Elm. Similar to how the strictness of the language pushes you to write code in a particular way, the Elm architecture pushes you to structure applications in a way that prioritizes maintainability.

The rest of this tutorial is meant to teach you what this means in practice. Piece by piece, you'll be building and extending an interactive user interface in Elm. By the end of the day, you should have a better sense of what it feels like to develop in Elm, and what it's like to work with a functional programming language.

Off we go!
