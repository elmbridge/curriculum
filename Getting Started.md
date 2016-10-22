# Getting Started

## Goals

  - Learn how to use the Elm REPL
  - Learn how to manipulate strings and numbers in Elm
  - Learn how to call functions
  - Learn where to find documentation about the Elm core library

## Steps

### <input type="checkbox"> Step 1

Launch the Elm REPL again by running the following command:

```sh
elm-repl
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

### <input type="checkbox"> Step 2

You can define and refer to variables:

```
> x = 5
5 : number
> y = 3
3 : number
> x + y
8 : number
```

### <input type="checkbox"> Step 3

You can concatenate strings using the `++` operator:


```
> "Hello" ++ ", World"
"Hello, World" : String
> name = "Anna"
"Anna" : String
> "Hello, " ++ name ++ "!"
"Hello, Anna!" : String
```

### <input type="checkbox"> Step 4

If you try to perform operations that don't make sense, Elm will try to tell you
what's wrong:

```
> 10 + "Betsy"
-- TYPE MISMATCH --------------------------------------------- repl-temp-000.elm

The right argument of (+) is causing a type mismatch.

3|   10 + "Betsy"
          ^^^^^^^
(+) is expecting the right argument to be a:

    number

But the right argument is:

    String

Hint: To append strings in Elm, you need to use the (++) operator, not (+).
<http://package.elm-lang.org/packages/elm-lang/core/latest/Basics#++>

Hint: I always figure out the type of the left argument first and if it is
acceptable on its own, I assume it is "correct" in subsequent checks. So the
problem may actually be in how the left and right arguments interact.
```

### <input type="checkbox"> Step 5

To call a function in Elm, you simply type the name of the function and any parameters you want to pass, separated by spaces.  No parentheses or commas are necessary.

Here are some of the functions that are available by default in Elm: `toString`, `max`, `min`, `sqrt`, `round`, `floor`.  These are defined in the `Basics` module, which is always imported for you. You can read more about these and other functions in [its documentation](http://package.elm-lang.org/packages/elm-lang/core/latest/Basics).

```
> toString 10 ++ "!"
"10!" : String
> min 9 1
1 : number
```

To disambiguate order of operations, use parentheses.

```
> round (96 / 7)
14 : Int
```

### <input type="checkbox"> Step 6

Let's use some functions from the [`String` module](http://package.elm-lang.org/packages/elm-lang/core/latest/String).

First, we need to import the module.


```
> import String
```

Then any function we want to use is namespaced under `String`:

```
> String.toUpper "Carey"
"CAREY" : String
> String.split "," "Apple,Apricot,Avocado,Banana,Blackberry"
["Apple","Apricot","Avocado","Banana","Blackberry"] : List String
> String.join " -- " (String.split "," "Apple,Apricot,Avocado")
"Apple -- Apricot -- Avocado" : String
```

### <input type="checkbox"> Step 7

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

### <input type="checkbox"> Step 8

Exit the Elm REPL by typing `:exit`, or `CTRL-D`.


### <input type="checkbox"> **Bonus!**

You may have noticed that all the types began with a capital letter (`String`, `Float`, `Int`) except for one (`number`). In general, you can remember that all types are capital but variables are lowercase. `number` in these cases is a special variable type saying the value can act as an `Int` or a `Float`. An example:

```
> 1 + 1
1 : number
> 1 + 1.0
2 : Float
> floor 1.3
1 : Int
> (floor 1.3) + 1.0
-- TYPE MISMATCH --------------------------------------------- repl-temp-000.elm

The right argument of (+) is causing a type mismatch.

3|    floor 1.3) + 1.0
                   ^^^
(+) is expecting the right argument to be a:

    Int

But the right argument is:

    Float
```
