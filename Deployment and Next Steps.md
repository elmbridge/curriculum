# Deployment and Next Steps

Since Elm code compiles to JavaScript, it can be very simple to host and deploy! There are lots of tools out there for hosting static websites composed of HTML, CSS, and JavaScript. For this tutorial, we'll use [Forge](https://getforge.com/), which is free for your first site!

## Goals

  - Deploy your Elm application for the world to see!
  - Learn about what's *not* covered in this tutorial, and how you can learn it

## Steps

### Deployment

Deploying a static site on Forge is relatively simple. Just follow these steps:

1. **Create an account at https://getforge.com/.** This should be absolutely free! Once you have an account, follow instructions to create a new, blank site.

2. **Compile your Elm application.** This is important! Since Forge only understands compiled JavaScript, any changes you've made to your app after your last compilation will not be reflected.  We have been using `elm reactor` for local development, but to create the final compiled application, we will need to use `elm make`.

   Run the following in your terminal:

   ```sh
   elm make Main.elm
   ```

   If you see `Successfully generated index.html`, then everything is ready to publish!

3. **Compress your project's folder into a .zip file.** The exact directions depend on your operating system, but it should be relatively straightforward on all platforms.

4. **Upload your new .zip file to Forge**. In a few seconds, your website should be ready.

You've just deployed your Elm application!

### Next Steps

Thank you for taking the journey with us! Hopefully, you now have an understanding of what it's like to be an Elm developer, and what it feels like to work with a functional, compiled language.

Before we finish, we should at least mention the things that this tutorial *didn't* cover, which will come up as you work more in Elm. Here's a non-exhaustive list:

- **Types and Type Signatures.** Elm allows developers to constrain and document their code using these tools. They are highly encouraged — a well-factored type system makes code more descriptive and more fault-tolerant. Once you've learned more about types, some of the more esoteric Elm compiler messages will begin to make more sense as well.
- **Currying and Piping**. Elm, like many functional languages, allows for functions to be partially applied. For example, if a function takes three arguments, you can give it one argument instead — and it will return a new function that takes two arguments! Elm developers use currying to reuse logic across their applications, and make their code more readable. In combination with the `|>` symbol (a.k.a. the pipe operator), currying can be a powerful tool.
- **Decoders, Commands, and Subscriptions**. Sometimes, it is necessary for an Elm application to talk to the outside world. You may need to parse JSON sent from your server, make an HTTP request to an API, use a third-party JavaScript library, or manipulate a part of the UI not rendered by your `view` function. In those cases, you will often have to tell Elm how to parse data it is receiving by using the `Json.Decode` module. You may also need to listen for changes to the outside world with `Subscriptions` or to trigger events outside of Elm using `Commands`.

There's so much to learn! Here are some resources to get you started:

  - [The official Elm guide](https://guide.elm-lang.org/) is a great resource, and gives a great rundown of some of the more complicated parts of the language.
  - [The elm-tutorial project](https://www.gitbook.com/book/sporto/elm-tutorial/details) is an incredibly in-depth tutorial on building a single-page app using Elm.
  - [The Elm Slack group](http://elmlang.herokuapp.com/) is a great way to get in touch with other developers learning and using Elm. We even have our own #elmbridge channel for you to connect with volunteers and fellow students. You can also check out http://elm-lang.org/community for more ways to get involved in the Elm community!

But more than anything, the best way to learn Elm is to write more Elm! You now know more than enough to write complex and rich front-end applications in the language, and you'll pick up nuances of the language as you go. Good luck!
