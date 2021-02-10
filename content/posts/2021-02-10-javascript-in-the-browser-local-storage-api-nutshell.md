---
template: post
title: "Javascript In The Browser: Local Storage API (Nutshell)"
slug: js-local-storage
socialImage: /media/javascript.png
draft: false
date: 2021-02-10T17:10:29.940Z
description: "The local storage API is used to store private/regular data within
  the browser. Typically, you'll see this come into play when dealing with
  authentication. "
category: JS Nutshell
tags:
  - javascript
  - coding
  - localstorage
  - frontend
---
# Intro

The local storage API is used to store private/regular data within the browser. Typically, you'll see this come into play when dealing with authentication. EX: user signs in successfully their user token will be stored in local storage to easily verify themselves later. Local storage data will remain there until you remove it manually, meaning closing the tabs and reopening data will persist. 



## Working with local storage 

the main methods to use when working with local storage.

* **setItem** -> sets an item in local storage
* **getItem** -> gets an item out of local storage
* **removeItem** -> remove item by key
* **clear** -> clear out all items

It can be access directly with by typing "localstorage" in the browser console.

**setItem(keyName, value)**

```javascript
// set the key and the value for the key
localStorage.setItem("name", "ajea")

```

**getItem(keyName)**

```javascript
// grab value by key name, in our case name
localStorage.getItem("name")
```

removeItem(keyName)

```javascript
localStorage.removeItem("name")
```

**clear()**

```javascript
localStorage.setItem("name", "ajea")
localStorage.setItem("age", "24")
localStorage.setItem("favColor", "blue")

// clears the storage
localStorage.clear()
```

Realistically, you'll want to store an array of objects of some sort, at least that's what I wanted to learn how to do lol. Before storing an array of data in localStorage, the data needs to be converted to a string like this. 

```javascript
const data = [
  {todo: "Buy Milk", completed: false}, 
  {todo: "Buy Juice", completed: false}, 
  {todo: "Buy Eggs", completed: true}
 ]

// convert data into string using JSON.stringify before storing in localstorage
localStorage.setItem("todos", JSON.stringify(data))
```

However, we need to convert it back to JSON using **JSON.parse()** in order to work with it. 

```javascript
// convert data back to JSON using JSON.parse
const todos = JSON.parse(localStorage.getItem("todos"))

console.log(todos)

```

Lastly, to get the count of local storage you can use the length property.

```javascript
localStorage.length
```

That's the localStorage API in a nutshell. Enjoy!