---
template: post
title: "Javascript In The Browser: Events (In A Nutshell)"
slug: js-events
socialImage: /media/javascript.png
draft: false
date: 2021-02-07T16:30:33.793Z
description: Events are like actions that is typically fired off by user interaction.
category: JS Nutshell
tags:
  - Javascript
  - coding
  - Events
  - frontend
---
Events are like actions that are triggered by user interactions. Ex: user fills out the form and clicks a button to submit data. In web apps, we always have some type of actions(Events) firing off. We also need to decide what happens next when these actions happen(Event Handlers)

Events come in different categories,

* Touch events: (for mobile devices) triggered when the trackpad around.
* Mouse events: triggered when either moving your mouse around the screen or clicking/double-clicking something.
* Keyboard events: triggered when pressing on some keys on the keyboard, e.g. (enter/return, delete, shift, a-z, etc.)
* Form events: triggered when form is submitted. 

There are many more, but listing all would be a turn off lol. However, you can find more on the [MDN website](https://developer.mozilla.org/en-US/docs/Web/Events) they list quite a bit. You could use any of these events depending on what you're building. 

The most common category(frequently used) are Mouse events and Keyboard events. Remind you these are just the categories. Let's look at the mouse events. 

Mouse Events (commonly used in web dev)

* Click (user clicked on something)
* DblClick (user double-clicked on something)

Form Events (commonly used in web dev)

* submit (user pressed submit button)

Now we need a way to listen out for these kinds of events, so we can do something afterward. The addEventListener method is used for this. 

Since we only have 1 button element, we don't have to use a class to reference it. 

Html file looks like this -> single button element

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Demo</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <button>Click for alert</button>
    <script src="main.js"></script>
  </body>
</html>
```

main.js file looks like this -> we use the addEventListener method to listen out for a click event on the button, then we call a function to say what we want to do afterward. In our case, alert a message.

```javascript
const button = document.querySelector("button");

button.addEventListener("click", () => {
  alert("hello world");
});

```

It would work just the same for Double clicks as well

```javascript
const button = document.querySelector("button");

button.addEventListener("dblclick", () => {
  alert("hello world");
});

```

Let's create a simple form, then listen for the submit event on a form element (do something when form is submitted). 

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
    <form>
      <input type="text" placeholder="email" />
      <input type="password" placeholder="password" />
      <button type="submit">submit</button>
    </form>
    <script src="main.js"></script>
  </body>
</html>

```

This time, we added the listener to the form element

```javascript
const form = document.querySelector("form");

form.addEventListener("submit", (event) => {
  // ignore this line, it's just something we have to add when working with forms
  event.preventDefault();
  console.log("form submitted");
});

```

The moral of the story is, there are many events you can listen out for and not just the ones I mentioned. You choose which element you want to listen to **(button, form, document itself)**, and then what event to listen out for **(click, dblClick, submit, keypress, etc.)**

This is also an [helpful article](https://flaviocopes.com/javascript-events/) on it if you want to dive deeper. Enjoy!