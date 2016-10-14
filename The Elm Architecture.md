# The Elm Architecture

![The Elm Architecture](images/elm-architecture-1.jpeg)

In this lesson, we'll run a simple Elm application, and learn how it all fits together!

## Goals

  - Run your first elm application.
  - Learn how every part of an elm application works.

## Steps

### <input type="checkbox"> Step 1

Download the Skeleton app here: [https://github.com/elmbridge/elmoji-translator/releases/tag/hello-world](https://github.com/elmbridge/elmoji-translator/releases/tag/hello-world) and navigate to the downloaded folder. Run the following command:

```sh
$ elm-make Main.elm --output dist/main.js
```

`elm-make` **compiles** your application — it turns your Elm code into JavaScript code that your browser can understand. The above command uses `Main.elm` as the **entry point** to your application — it compiles that file, along with any files it references, and dumps the output into a file called `main.js`. This file is loaded in `index.html`, which then kicks off your elm application using JavaScript.

Whenever you make a change to your code, you will have to recompile before those changes are reflected in your browser. If your code is broken in someway, `elm-make` will fail, and give you helpful error messages on what you need to fix.

Now run the following command to open the application in your browser:

```sh
$ open index.html
```

You should now have a fully functional elm application, that looks like this:

![Hello World](images/hello-world.gif)

### <input type="checkbox"> Step 2

So how does any of this work? We'll, let's start off in `Main.elm`, which, (by convention) is the entry point to an Elm application.


```elm
main =
    Html.App.beginnerProgram
        { model = Model.init
        , view = View.view
        , update = Update.update
        }
```

The `main` function describes the initialization logic for your Elm application. Every entry point file requires `main` function. It consumes a record with three basic pieces of every Elm application:

- **The initial `model`**, which describes the state of our application. The value of `model` will change as the user interacts with our application.
- **The `view` function**, which is responsible for converting a `model` into HTML for elm to render to the UI. It also maps all possible user actions to the appropriate `messages`.
- **The `update` function**, which is responsible for updating the application's state based on triggered `messages`. It consumes the current application state (the `model`) a single `message`, and returns a new `model` that describes the application's new state.

![The Elm Architecture](images/elm-architecture-4.jpeg)

The initial `model`, `view` function, and `update` function together form a **triad** that is required in every Elm application. For more complicated programs, a few other peices are required — however, for this session, we'll focus on the core triad.

### <input type="checkbox"> Step 3

Let's investigate each of these pieces one by one. First, let's check out the `init` function in `Model.elm` to see what the initial state of our application is.

```elm
init =
    { text = "hello world!" }
```

As you can see, `Model.init` takes no arguments and returns a **record**, which is a key-value map with predefined keys. This particular record has a single key called `text`, with a value of `"hello world!"`. This record represents the state of or application — it is the only thing that can change in the entire system. As the `model` changes, the UI should change to reflect it's new value.

It is convention to write a **type alias** to describe your application's state, and call it `Model`, like this:

```elm
type alias Model =
    { text : String }
```

We'll learn more about type aliases later in this tutorial, but for now, it's worth noting that it is simply used for convenience. It's an easy way for other elm developers to tell exactly what information is stored in your `model`.

### <input type="checkbox"> Step 4

Now, let's take a look at our `view` function in `View.elm`, which is responsible for converting our `model` into HTML. Any changes between the produced HTML and the last rendered HTML will be rendered to the UI by elm.

```elm
view model =
    Html.div
        [ Html.Attributes.class "skeleton-elm-project" ]
        [ Html.div
            [ Html.Attributes.class "waves-effect waves-light btn-large"
            , Html.Events.onClick Update.ChangeText
            ]
            [ Html.text model.text ]
        ]
```

If you have worked with Angular, React, Ember, or another front-end framework, this part may seem somewhat familiar to you. Every front-end framework has it's own syntax for describing HTML, and Elm is no different. The subsequent HTML looks like this:


```html
<div class="skeleton-elm-project">
  <div class="waves-effect waves-light btn-large">
    hello world!
  </div>
</div>
```

The `view` function uses the `Html` module to render HTML nodes. `Html.div` is a function that consumes two lists — a lite of attributes, and a list of children. Our first div has one attribute (a `class` attribute that provides a class for styling) and it has another div as it's child.

The child div has two attributes (another `class` attribute and an `onClick` handler). This div has one child: a plain text html node, rendered using the `Html.text` function.

What does `model.text` means in the context of our `view` function? This function is responsible for rendering the application's current state as HTML — and that state is stored in the `model` variable. Every time the application's state changes, this function will be called with a new `model` value — if `model.text` is different than the last time this function was called, the UI will update with new text!

You may wonder how this function can be performant — every time the `model` changes, even slightly, our `view` function has to recalculate every HTML element in your application. If you have hundreds of elements, and dozens of potential changes, How does elm not collapse under the load?

Good news: Elm is optimized to be performant under pressure. It uses a library called [virtual-dom](https://github.com/elm-lang/virtual-dom) to ensure that the entire page doesn't have to re-render every time the application's state changes. React and Ember use similar strategies, although Elm has more tricks up it's sleeve because of it's functional nature. The exact details are out of scope for this tutorial, however — just know that you generally don't have to worry about performance when writing elm.

Before we move on, let's take another look at that `onClick` handler:

```elm
Html.Events.onClick Update.ChangeText
```

This line of code is key to our application — it maps a potential user action to a `message` that can cause our application to change. In this case, clicking on our div causes the the `Update.ChangeText` message to be sent.

There are lots of potential user actions defined in the [`Html.Events`](http://package.elm-lang.org/packages/elm-lang/html/latest/Html-Events) library — as with JavaScript, you can track when a user clicks an element, or presses a key, or submits a form. If you don't map these user actions to a `message`, however, they will ignored by your application.


### <input type="checkbox"> Step 5

Now to the final piece of our application — the `update` function. This function is responsible for consuming `messages` triggered by the user. It takes the current `model`, the triggered `message`, and returns a new `model` for the `view` function to render.

```elm
update msg model =
    case msg of
        ChangeText ->
            if model.text == "hello world!" then
                { model | text = "goodbye world!" }
            else
                { model | text = "hello world!" }
```

We just saw that the `ChangeText` message can be triggered in the UI when the user clicks our button. When a message is sent, this function applies some conditional logic:

- If the current application's state (stored in the `model` variable) has a `.text` value of `"hello world!"`, the function return a new `model` with a value of `"goodbye world!"`.
- If `model.text` is *already* set to `"goodbye world!"`, this function returns a `model` with a `text` value  of `"hello world!"`.

Either way, the new `model` will be converted to HTML, and any changed will be rendered to the UI by our `view` function.

Wait, there's only one possible action tracked in our UI — why have a case statement at all?  This is convention in elm-land. As you build an application, there will be more and more kinds of `messages` to which your `update` function will have to react. Consequently, this case statement will get longer and longer to accomodate the new messages.

It's worth taking a look at `Msg` type:

```elm
type Msg
    = ChangeText
```

This is a **union type** declaration in elm. We'll go further into the details in a future lesson, but for right now, you can think of this as way to model `messages` in our application. The above code declares that there is exactly one acceptable value for a `message`: a value called `ChangeText`. If we wanted to add another `message`, we would have to change this declaration to include a new value for `Msg`.

Elm doesn't enforce that we use a union type called `Msg` for `messages` — we could just as easily model `messages` as strings, or numbers, or records. It is convention, however, to model data using union types whenever appropriate. Don't worry if you are somewhat lost — union types are one of the more difficult concepts to learn as a beginner to elm, and it's fine for now if they are simply magic words you know you can recite.

Now that we're done touring the basics of the elm triad, let's get building!
