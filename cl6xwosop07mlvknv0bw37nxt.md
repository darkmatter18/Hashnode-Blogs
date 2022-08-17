## Create your first NPX script

You might use the npx command many times if you are a JavaScript developer.
There are many well-known npx commands on the globe, like `npx create-react-app`, which will help you create a new ReactJs project. 

## So what is NPX?

From NodeJs [documentation](https://nodejs.dev/learn/the-npx-nodejs-package-runner): "`npx` lets you run code built with Node.js and published through the npm registry."

So in simple words, npx helps you to run npm packages directly from the npm registry. You don't need to install the package in a `node_modules` folder separately and don't have to run it separately. npx will do all for you.

You'll feel like, you are running a `bash` script. But under the hood, it's an npm package.

## So let's create an NPM package

To start building your npx script, you first need to create a normal NPM library. 

You can follow this tutorial to know how to create an NPM Package https://www.section.io/engineering-education/npm-packages/

Create a name for your library as per your need. Remember the name must have to be globally unique.

We don't need to install libraries in the package, we have it simple for now. 

After you have done creating the npm package, you must have 2 files there

1. `package.json`   <- Contains the metadata of the package
2. `index.js`            <- Entrypoint for the package

## Make required changes in the package.json

1. **Add the Main entry point**

```json
"main": "index.js",
```
It will make the `index.js` run when the package is called.

2. **Add the bin entry point**

```json
"bin": {
    "<package_name>": "index.js"
},
```

It will help npx to identify, which file it needs to execute when called.

A complete package.json will look something like this. 

%[https://gist.github.com/16c1daba797956fc86dec2b9dbbe23b2]

## Now it's time for index.js

- Start your `index.js` file with a `#!/usr/bin/env node`. It'll help the underlying shell to understand which executable it should use.

- (Optional but Recommended) After that, use `'use strict'` to go into the strict mode

Now you can do whatever you want to do with it. It's now all yours. 

**You can use it as 1. Portfolio Card, 2. Build small games, 3. Show your blogs here. Use your imagination, and do whatever you like.**

An example of `index.js`

%[https://gist.github.com/darkmatter18/d3237180eb6cb06cda1968024a69133c]

Hooooraaaaay 🎉🎉🎉

You build your first NPX script.

## Testing
Before testing, publish the changes you did by using `npm publish`.

Now to test, use
```bash
npx my_awesome_package
```

It should print
```bash
Hello World
```

Thanks a LOT. 🙌