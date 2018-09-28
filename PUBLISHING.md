## How to publish this gitbook

You will need NodeJS 10 or later.

Make sure you have the gitbook CLI installed:

```sh
npm install gitbook-cli
```

Rebuild the gitbook, commit, and push:

```sh
npx gitbook build . docs
git add docs
git commit
git push
```
