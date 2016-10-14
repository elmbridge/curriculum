# Making it Dynamic

In this release, we'll start making our emoji translator app! Eventually, the app will be able to "encrypt" messages using an emoji key, so that users can pass secret messages to each other. The final product will look something like this:


![Final Release](images/final-release.png)


We need to walk before we run, though! First, we'll make an application that simply consumes text input provided by the user and displays it back to the page.

## Goals

  - Download and run the Skeleton Elmoji app.
  - Understand how to use Elm to make things change on the page.

## Steps

### <input type="checkbox"> Step 1

Download the Skeleton app here: [https://github.com/elmbridge/elmoji-translator/releases/tag/release-0](https://github.com/elmbridge/elmoji-translator/releases/tag/release-0) and navigate to the downloaded folder. Run the following commands to open the app in your browser:

```sh
$ elm-make Main.elm --output dist/main.js
$ open index.html
```

You should now have a fully functional elm application running in your browser! It should look like this:

![Release 0](images/release-0.png)

### <input type="checkbox"> Step 2

As you may have already noticed, however, this Elm application doesn't *do* anything. While you can enter text on the page, the application seems to ignore it.

Our goal is to make the text that the user enters display back to them, like this:

![Release 1 in GIF form](images/release-1.gif)

As we learned in [the last lesson](The Elm Architecture.md), every Elm app is built upon the `Model`, `View`, and `Update` triad. This app is no different – in order to implement this feature, we may need to change all three.

First, Let's take a look at the model in `Model.elm`:


```elm
type alias Model =
    { currentText : String }
```

This model represents the state of the application. All changes on the page should be reflections of a change in this model. This model is a **record**, which is a key-value map with predefined keys. In our case, the model contains a `currentText` attribute that must be a string. That's perfect for our feature — as a user inputs text into the application, we'll update the `currentText` attribute, and reflect it's new value to the UI.

Let's verify that user text input is being captured, and triggering an update to the model. First, let's look in `View.elm`, which is much bigger than it was in the last release! Specifically, let's take a look at the code for input field.

```elm
Html.input
  [ Html.Attributes.type' "text"
  , Html.Attributes.class "center"
  , Html.Attributes.placeholder "Let's Translate!"
  , Html.Events.onInput Update.SetCurrentText
  ]
  []
```

It's worth taking a moment to discuss the API for the `HTML` module. almost all functions in this module have the same structure -- they consume a list of html attributes (like `class`, `id`, `display`, etc.) as well as a list of child elements that are nested inside them.

While the API is somewhat verbose, much of its contents are probably familiar to you. In this case, the code is generating an `input` element with a type of `text` and a class of `center` and some placeholder text. The resulting HTML looks like this:

```HTML
  <input type="text" class="center" placeholder="Let's Translate!">
```

The final attribute comes from the HTML.Events library, which describes which `Update` message is sent when the element hears an `input` event. In this case, a message called `SetCurrentText` is sent, along with the element's current text. (SetCurrentText is actually a parameterized type -- don't worry, we'll cover that in a future lesson!)

This is great! When this message is sent, we can update our model with the new value. To do that, let's check out `Update.elm`:

```elm
update msg model =
    case msg of
        SetCurrentText newText ->
            -- currently, this does nothing!
            model
```

Whenever an update message is sent, the `Update.update` function consumes the sent message, the current model, and returns a new model to render. Currently, the `SetCurrentText` message is handled by this function, but the function simply returns the old model.

Let's change that. Instead, we should have the update function to update the model's `currentText` value whenever the message `SetCurrentText` is sent. Let's use record update syntax to do so:

```elm
update msg model =
    case msg of
        SetCurrentText newText ->
          { model | currentText = newText }
```

once you've made the change, recompile your code by running the following:

```sh
$ elm-make Main.elm --output dist/main.js
```

The compiler will tell you about any errors you made, or let you know that everything is working!

### <input type="checkbox"> Step 3

Great, so we're now updating the model every time the user inputs text into our application. However, that's only half the battle — we still need to display the applications `currentText` back to the user!

Thankfully, the skeleton already includes some styling for us. All we need to do is add code to our `View.view` function to display a paragraph tag right after our input tag, with the model's `currentText` as it's value. The resulting HTML should look like this:


```HTML
  <p class="center output-text emoji-size">It's happening!!!</p>
```

In elm, the code to generate that HTML would look like this

```elm
Html.p
    [ Html.Attributes.class "center output-text emoji-size" ]
    [ Html.text "It's happening!" ]
```

Note: `HTML.text` is a special kind of `HTML` function, that produces a plain-text node. In this case, we've built a paragraph HTML element with a nested child element that is simply plain text.

Insert the above code into the `View.view` function, as a list element after the `HTML.input` element. Once you think you have it, recompile your code to see if it worked.

### <input type="checkbox"> Step 4

We don't want the text to always be `It's happening!`, though. Instead, the text of the paragraph node should reflect the `currentText` of the current model. As the model changes, this paragraph node should change as well.

You'll notice that the `View.view` function consumes a model. This model represents the current state of the application! So if we use record getter syntax, we can pull the `currentText` value out of the model and use it, like this:

```elm
Html.p
    [ Html.Attributes.class "center output-text emoji-size" ]
    [ Html.text model.currentText ]
```

Recompile your code, refresh your browser, and you should have a fully functional, dynamic application!
