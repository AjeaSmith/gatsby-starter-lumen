---
template: post
title: "Javascript In The Browser: Forms (Nutshell)"
slug: js-forms
socialImage: /media/javascript.png
draft: true
date: 2021-02-11T01:06:43.881Z
description: Forms are an essential part of web development. It's rare that you
  come across a website and don't see a form of some sort, they're everywhere
  (contacts, search bars, signup/sign in, etc.).
category: JS Nutshell
---
# Intro

Forms are an essential part of web development. It's rare that you come across a website and don't see a form of some sort, they're everywhere(contacts, search bars, signup/sign in, etc.).

## How forms work without Javascript (Default behavior)

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
    <form action="/success" method="POST">
      <input type="email" name="email" placeholder="enter email" />
      <input type="password" name="password" placeholder="enter password" />
      <button type="submit">submit</button>
    </form>
    <script src="main.js"></script>
  </body>
</html>

```

By default, when forms are submitted they make a post request to the page url (on the same origin) we're currently on. This makes the form data visible in the URL address bar for the world to see, of course this not what we want.

So, to override this behavior we need to specify a url to make a post request to. We do this using the **action** and **method** attributes.

**action**: tells which url to make post request to

**method**: which type of request method 

The button with **type="submit"** will automatically submit the form. 

## How forms work with Javascript

You could keep the action and method attributes, but I'm going to remove it for this demo. 

```javascript
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
      <input type="email" name="email" placeholder="enter email" class="email"/>
      <input type="password" name="password" placeholder="enter password" class="password"/>
      <button type="submit">submit</button>
    </form>
    <script src="main.js"></script>
  </body>
</html>

```

We added classes this time for the **email** and **password** inputs. We did this because we need a way to access these elements in our JS file, then grabs its values. 

```javascript
const form = document.querySelector("form");
const email = document.querySelector(".email").value
const password = document.querySelector(".password").value

form.addEventListener("submit", (event) => {
  event.preventDefault();
  console.log({ email: email, password: password });
});

```

Here, we appended the **value** property to get access to the values of the **email** and **password** inputs. Then, we added a submit event listener to the form element. We called **event.preventDefault()** to prevent the form from submitting and doing the default behavior I mentioned before, this way we have full control over form submission. 

Lastly, we **console.log()** our email and password values to see what was submitted. In a real world scenario, we would save the email and password to a DB of some sort. 

That's the basic of forms, in a nutshell. Enjoy! :)