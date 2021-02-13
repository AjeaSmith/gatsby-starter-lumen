---
template: post
title: "Babel: JS Dev Tools"
slug: js-babel
socialImage: /media/babel-js.png
draft: false
date: 2021-02-11T20:43:24.382Z
description: Babel is a tool that converts new JS features into a different
  standard version for older browsers to use.
category: JS Dev Tools
---
# Intro

Babel allows developers to use the latest JS syntax. Babel plugins help transpile the latest syntax to an older version for older browsers to read. Therefore, you don't have to wait for browser support, the plugins will do the transpiling for you behind the scenes.

## Installing Babel 

```
npm install --save-dev @babel/core @babel/cli
```

For EX: for use to use arrow functions, this is the plugin to use for older browsers. In a nutshell, this plugin (below) will look at any code with arrow functions and convert it into regular functions for older browsers to read. 

```
npm install --save-dev \
    @babel/plugin-transform-arrow-functions
```

Once we have the plugin installed, we need to add it to our **.babelrc** file which is like our configuration file for babel plugins. Create a **.babelrc** file in root project folder.

```
{
  "plugins": ["@babel/plugin-transform-arrow-functions"]
}

```

Let's create a script for babel (in our **package.json** file) so when we run it, it'll do the transpiling. You need to name the file you need to be transpiled, in our case the **main.js** file. 

```
"scripts": {
    "babel": "babel main.js"
 }
```

## Code with an arrow function

![With an arrow function](/media/screen-shot-2021-02-12-at-3.13.26-pm.png "With an arrow function")

## Babel transpiled (script: npm run babel)

![Babel transpiled code](/media/screen-shot-2021-02-12-at-3.14.09-pm.png "Babel transpiled code")

As you can see, the arrow function is now a regular function which older browsers support.

# Babel Presets

They are sets (groups) of babel plugins that support different features. It's much easier to get a babel preset than to install hundreds of single plugins. 

## Common Presets

1. env preset
2. react preset

### env preset

Complies code from es15 - latest versions. You could specify which browser you want support for, but most of the time you'll support all. You need to install the env preset. 

```javascript
npm install --save-dev @babel/preset-env

// this goes into .babelrc file
{
  "presets": ["@babel/preset-env"]
}
```

### react preset 

Complies JSX code, making it easier to work with react projects

```javascript
npm install --save-dev @babel/preset-react

// this goes into .babelrc file
{
  "presets": ["@babel/preset-react"]
}

```

This is the basic level behind babel. Enjoy!