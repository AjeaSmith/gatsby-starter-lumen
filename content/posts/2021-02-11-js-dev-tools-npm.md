---
template: post
title: "JS Dev Tools: NPM"
slug: js-npm
socialImage: /media/javascript.png
draft: false
date: 2021-02-11T03:30:49.147Z
description: NPM stands for Node Package Manager. It's a package registry that
  stores all different kinds of packages you can use in your applications that
  other people created to save developers time from writing the code themselves
  from scratch. There is a package for almost anything nowadays (validation,
  animation, etc.).
category: JS Dev Tools
tags:
  - javascript
  - coding
  - npm
  - frontend
---
# Intro

NPM stands for Node Package Manager. It's a package registry that stores all different kinds of packages you can use in your applications that other people created to save developers time from writing the code themselves from scratch. There is a package for almost anything nowadays (validation, animation, etc.).

## Install Packages from NPM

```javascript
// installs package into your project 

npm install <package-name>
```

There are two places the package will be placed in (**dependencies** or **devDependencies**).

**dependencies**: are packages that we need to use in development and production. 

**DevDependencies**: are packages we only need in development. 

## Save in **dependencies**

```
npm install <package-name> --save
// or 
npm install <package-name>
```

## Save in devD**ependencies**

```
npm install <package-name> --save-dev
```

## Package.json file

When you install packages, they're listed here under the sections **dependencies** and **devDependencies.** it's an object with your project information, along with which versions of the packages you installed. Below is an example of what a package.json would look like (sample file from a project I'm working on lol)

```
{
  "name": "awesome-project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "nodemon server.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "nodemon": "^2.0.7",
    "sequelize-cli": "^6.2.0"
  },
  "dependencies": {
    "apollo-server": "^2.19.2",
    "bcryptjs": "^2.4.3",
    "graphql": "^15.5.0",
    "jsonwebtoken": "^8.5.1",
    "mysql2": "^2.2.5",
    "sequelize": "^6.4.0"
  }
}
```

## Uninstalling packages

```
npm uninstall <package-name>
```

## Uninstalling development dependencies

```
npm uninstall -D <package-name>
```

## Updating Packages

```javascript
npm outdate // find packages that are out of date

npm install // update all packages to their major versions

npm install <package-name>@latest // update specific package
```

## Global Installs

```javascript
// global installs the package in root dir of node
npm install <package-name> -g

```

I don't want to dive too deep, but this is ground level of what NPM is about. Enjoy! :)