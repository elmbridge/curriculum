# Emojification

Up until now, this project has had a severe lack of emojis. In this release, we'll learn how to use an external module to translate text into emojis. Once we're done, it should look something like this:

![Release 2](images/release-2.png)


Your code should currently [look like this](https://github.com/elmbridge/elmoji-translator/tree/release-1). You can either carry your code over from the last release, or download and recompile [the code from GitHub.](https://github.com/elmbridge/elmoji-translator/releases/tag/release-1)


## Goals

  - Access and utilize code in other modules
  - Be able to write helper functions
  - Understand where to locate domain-specific code

## Steps

### <input type="checkbox"> Step 1

Spoiler alert: Emojis are complicated! And creating a decoder-ring-style translator between plain text and emojis is no small feat. Thankfully, one of your teammates has already written an emoji converter library for you to use, so you don't have to deal with that complexity! The code is already in your skeleton, in `EmojiConverter.elm`.

We'll need to use that code to convert the display text from plain text to emojis. But how do we pull that code in to our `View.elm` file?

That's where the Elm **module** system comes into play. Modules are simply collections of related functions. They are helpful for encapsulating behavior, and for providing clear boundaries between libraries. Let's take a look at the first few lines of `EmojiConverter.elm`:

```elm
module EmojiConverter exposing (textToEmoji, emojiToText, supportedEmojis)
```

Like all Elm files, `EmojiConverter.elm` starts off by telling us what module it defines. In other files, we'll be able to call its functions by using the `EmojiConverter` namespace, in the same way we use the `Html` or `List` namespaces.

This line also tells us the public API for the `EmojiConverter` module — regardless of what else is defined in this file, other files can, at most, access the three functions defined above. We can make some guesses as to purpose and signature for these functions, based on their names. In this case, the `textToEmoji` function seems like exactly what we are looking for.

Let's import just the module into our `View.elm` file, by adding this to the list of imports:

```elm
import EmojiConverter
```

Now let's try using the `textToEmoji` function in our output text section.


```elm
Html.p
    [ Html.Attributes.class "center output-text emoji-size" ]
    [ Html.text (EmojiConverter.textToEmoji model.currentText) ]
```

Let's try to compile this, and...uh oh! You should be getting the following error:

```sh
==== error in View.elm:40:19: ====
The argument to function `text` is causing a mismatch.
Function `text` is expecting the argument to be:
    String
But it is:
    String -> String
```

This error might seem like gibberish at first, but stay strong — Elm error messages are very good at telling you exactly what you need to know. In this case, it seems that, instead of passing `HTML.text` a string to render, we are passing it a function that takes a string and returns a string. In Elm-land, that often means that you passed too few arguments into a function — if a function takes two arguments, and you only provided it one, it will return a **partially-applied function** that still needs one more argument!

As you may have guessed, it seems like we've gotten the signature for `EmojiConverter.textToEmoji` wrong. Let's take a look at its definition in `EmojiConverter.elm`:

```elm
type alias Key =
    String


textToEmoji : Key -> String -> String
textToEmoji key text =
  ...
```

Apparently, `textToEmoji` takes two arguments — a `Key` and a `String`, and returns a converted `String`. If we look a few lines above in the file, we see that `Key` is simply an alias for `String`.

Of course! Like any good decoder ring, the `EmojiConverter` library uses a key to determine how to encode and decode messages. In this case, the key can be one of the emojis supported by the library. In order to turn text into emojis, we need to give it a key, as well as the text we hope to translate.

Let's go back to `View.elm`, and hard-code an emoji as the translation key.


```elm
Html.p
    [ Html.Attributes.class "center output-text emoji-size" ]
    [ Html.text (EmojiConverter.textToEmoji "😅" model.currentText) ]
```

Recompile the code, refresh your browser, and you should be in business!

### <input type="checkbox"> Step 2

While this solution works, I'd argue that the code has become harder to follow. Let's refactor!

First off, let's extract a helper function for translating text. in `View.elm`, we can add a function that consumes a model and returns emojis:

```elm
translateText model =
    EmojiConverter.textToEmoji "😅" model.currentText
```

Note: Type signatures are always optional in Elm, but they are highly encouraged — type signatures can be a good form of documentation, and they help the compiler make educated guessed about what went wrong when your code fails to recompile. Feel free to add your own to `translateText`!

We can now use this function in our `View.view` function. Since it's defined in the same file as it's being used, we don't even have to use the `View` namespace. We can simply invoke it as such:

```elm
Html.text (translateText model)
```

Recompile your code and make sure everything still works!

### <input type="checkbox"> Step 3

Finally, let's pull out the hard-coded emoji key into something more readable. Since the key denotes domain-specific information about your app, the best place to put that information would be in `Model.elm`. Remember, modules in Elm are simply collections of functions that are similar to each other. Just because we put a function in `Model.elm` doesn't mean it has anything to do with our model record, or with application state in general.

Let's create a `defaultKey` function in `Model.elm` that simply returns the "😅" emoji. Since Model.elm includes `exposing (..)` in its definition, we don't need to explicitly white-list our new `defaultKey` function for export — all other files can access all functions in this file if requested.

Finally, let's use our `defaultKey` function. In `View.elm`, switch out the reference to the "😅" emoji key with references to the new `defaultKey` function.

Once you think you've got it, recompile to make sure it worked. If you get stuck, check out [the completed release](https://github.com/elmbridge/elmoji-translator/tree/release-2) on GitHub to see how we've implemented it.
