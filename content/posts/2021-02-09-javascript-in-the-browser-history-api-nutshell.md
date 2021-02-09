---
template: post
title: "Javascript In The Browser: History API (Nutshell)"
slug: js-history-api
socialImage: /media/javascript.png
draft: false
date: 2021-02-09T20:42:13.801Z
description: "The history API's main job is to handle the navigation between
  pages (forward, backward, changing content in the address bar). You can access
  the history API directly by typing \"history\" in the browser console. "
category: JS Nutshell
tags:
  - Javascript
  - coding
  - frontend
  - historyapi
---
# Intro

The history API's main job is to handle the navigation between pages (forward, backward, changing content in the address bar). You can access the history API directly by typing history in the browser console. 

## \
Navigating through pages

* **back** (goes back a page) -> **history.back()**
* **forward** (goes to next page) -> **history.forward()**
* **go** (navigate back or forward) -> **history.go(2) goes forward 2 pages, history.go(-1) goes back 1 page**
* **pushState** (goes to new page and the option to pass any data if needed.) -> 

  ```javascript
  const button = document.querySelector("button");

  // data passed to history state
  const state = { email: "johndoe@mail.com", password: "12345" };

  button.addEventListener("click", () => {
    // passes data to "/user" page
    history.pushState(state, "", "/user");
  });
  ```
* **replaceState** (replaces the current page with the one you specified)

  ```javascript
  const button = document.querySelector("button");

  // data passed to history state
  const state = { email: "johndoe@mail.com", password: "12345" };

  // current page
  history.pushState(state, '', '/currentPage')

  button.addEventListener("click", () => {
    // passes data to "/user" page
    history.replaceState(state, "", "/newPage");
  });
  ```

  At the moment our current page is **'/currentPage'**. However, once we click the button the **'/newPage'** will now be our current page. At this point, you could use the **history.back()** to go back a page, in our case it would go to **'/'.** 

  To access the state you passed in **pushState** and **replaceState** use -> **history.state**. It will show the data you passed in. 

  Our simple html file -> 

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Demo</title>
      <link rel="stylesheet" href="style.css" />
    </head>
    <body>
      <button>Go to next page</button>
      <script src="main.js"></script>
    </body>
  </html>

  ```

  This one was short and sweet, as you can see the history API is actually not complicated at all :) Enjoy!