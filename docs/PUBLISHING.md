## How to publish this gitbook

Make sure you have the gitbook CLI installed:

```sh
npm install -g gitbook
```

Make sure you are on the latest master branch:

```sh
git checkout master
git pull
git status
```

Do a clean rebuild of the gitbook:

```sh
rm -Rf _book
gitbook build
```

Checkout the gh-pages branch:

```sh
git checkout gh-pages
```

Move the gitbook output to the top-level, and commit:

```sh
rsync -va _book/ ./
git add .
git status # make sure everything looks okay
git commit -m "Publish `cat .git/refs/heads/master`"
```

Push the `gh-pages` branch:

```sh
git push gh-pages
```

You're done!  Switch back to `master` so you won't be confused in the future:

```sh
git checkout master
```
