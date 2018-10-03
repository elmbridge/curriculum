# Installation Notes for Windows Users

If you are running Windows on your machine, you might find this checklist of activities helpful:

* Before running the Windows installer, shut down your command prompt (`cmd.exe`) and/or Cygwin applications.
* After running the installer, you will also need to install `nodejs`, from the [Node JS](https://nodejs.org/) website. You can choose the option that says "Recommended For Most Users."
* After completing the NodeJS installation, open a new command prompt (or Cygwin) window and type in `elm repl` at the command line. If you _don't_ see this message, you are good to go! If not, consult an instructor or TA:

```
$ elm repl
The REPL relies on node.js to execute JavaScript code outside the browser.
I could not find executable 'node' or 'nodejs' on your computer though!

You can install node.js from <http://nodejs.org/>. If it is already installed
but has a different name, use the --interpreter flag.
---- Elm 0.19.0 ----------------------------------------------------------------
Read <https://elm-lang.org/0.19.0/repl> to learn more: exit, help, imports, etc.
--------------------------------------------------------------------------------
```
