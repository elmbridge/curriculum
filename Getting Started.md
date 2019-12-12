# Getting Started

## Goals

  - Learn how to use the Elm REPL
  - Learn how to manipulate strings and numbers in Elm
  - Learn how to call functions
  - Learn where to find documentation about the Elm core library

## Steps

### REPL

Launch the Elm REPL again by running the following command:

```sh
elm repl
```

Now that you are in the REPL, you can write your first Elm code! Code you should try out in the REPL is written on lines starting with `>`.

You can enter values, and Elm will tell you the type of the values.  Try typing
strings, numbers, and simple mathematical expressions:

```
> "Hello"
"Hello" : String
> 100
100 : number
> 100.5
100.5 : Float
> 50 / 7
7.142857142857143 : Float
> 4 + 3 * (6 - 2)
16 : number
```

### Variables

You can define and refer to variables:

```
> x = 5
5 : number
> y = 3
3 : number
> x + y
8 : number
```

### Strings

You can concatenate strings using the `++` operator:


```
> "Hello" ++ ", World"
"Hello, World" : String
> name = "Anna"
"Anna" : String
> "Hello, " ++ name ++ "!"
"Hello, Anna!" : String
```

### Error Messages

If you try to perform operations that don't make sense, Elm will try to tell you
what's wrong:

```
> 10 + "Betsy"
-- TYPE MISMATCH ----------------------------------------------------------- elm

I cannot do addition with String values like this one:

7|   10 + "Betsy"
          ^^^^^^^
The (+) operator only works with Int and Float values.

Hint: Switch to the (++) operator to append strings!
```

### Functions

To call a function in Elm, you simply type the name of the function and any parameters you want to pass, separated by spaces.  No parentheses or commas are necessary.

Here are some of the functions that are available by default in Elm: `max`, `min`, `sqrt`, `round`, `floor`.  These are defined in the `Basics` module, which is always imported for you. You can read more about these and other functions in [its documentation](http://package.elm-lang.org/packages/elm-lang/core/latest/Basics).

```
> max 9 1
9 : number
> min 9 1
1 : number
```

To disambiguate order of operations, use parentheses.

```
> round (96 / 7)
14 : Int
```

### The String Module

Let's use some functions from the [`String` module](http://package.elm-lang.org/packages/elm-lang/core/latest/String), which is one of the modules imported by default.

Any function we want to use is namespaced under `String`:

```
> String.fromInt 10 ++ "!"
"10!" : String
> String.toUpper "Carey"
"CAREY" : String
> String.split "," "Apple,Apricot,Avocado,Banana,Blackberry"
["Apple","Apricot","Avocado","Banana","Blackberry"] : List String
> String.join " -- " (String.split "," "Apple,Apricot,Avocado")
"Apple -- Apricot -- Avocado" : String
```

### Importing Modules

If we want to use functions in a module that isn't available by default, we need to first import the module.

```
> import Bitwise
```

Functions in the `Bitwise` module are namespaced under `Bitwise`:

```
> Bitwise.and 7 2
2 : Int
```

### Defining our own Functions

Now let's define and use our own functions.

We saw types before when we entered numbers and Strings into the console; functions have types too!

When Elm shows the type of a function, it uses arrows `->` and colons `:`. We've seen the colons already, when Elm told us the types of values (e.g., `14 : Int`).

The arrows point to the return value.  Generally, the rightmost type is the return value, and the other types are the parameters to the function.  For example, `Int -> String -> Float` is the type of a function that takes two parameters: the first is an Int, the second is a String, and the function returns a Float.

```
> multiplyByThree x = x * 3
<function> : number -> number
> multiplyByThree 10
30 : number
> add a b = a + b
<function> : number -> number -> number
> add 10 4
14 : number
> sayHello name = "Hello, " ++ name
<function> : String -> String
> sayHello "Janice"
"Hello, Janice" : String
```

> **Note:** If you get a `SHADOWING` error in the Elm REPL from previously defining `x`, you can type `:reset` to clear all previous imports and definitions.

### All done!

Exit the Elm REPL by typing `:exit`, or `CTRL-D`.


### **Bonus!**

You may have noticed that all the types began with a capital letter (`String`, `Float`, `Int`) except for one (`number`). In general, you can remember that all types are capital but variables are lowercase. `number` in these cases is a special variable type saying the value can act as an `Int` or a `Float`. An example:

```
> 1 + 1
1 : number
> 1 + 1.0
2 : Float
> floor 1.3
1 : Int
> (floor 1.3) + 1.0
-- TYPE MISMATCH ---------------------------------------------------------- REPL

I need both sides of (+) to be the exact same type. Both Int or both Float.

4|   (floor 1.3) + 1.0
     ^^^^^^^^^^^^^^^^^
But I see an Int on the left and a Float on the right.

Use toFloat on the left (or round on the right) to make both sides match!

Note: Read <https://elm-lang.org/0.19.1/implicit-casts> to learn why Elm does
not implicitly convert Ints to Floats.
```
