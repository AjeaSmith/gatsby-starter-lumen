---
template: post
title: "Javascript In The Browser: Networking (Nutshell)"
slug: js-networking
socialImage: /media/javascript.png
draft: false
date: 2021-02-08T18:59:42.733Z
description: Network requests happen very often in web apps. The flow consists
  of using some request API (XHR, fetch, Axios) to interact with the server to
  fetch some data, then return it to us in a format we can understand and work
  with (JSON).
category: JS Nutshell
tags:
  - Javascript
  - coding
  - networking
  - frontend
---
# Intro

Network requests happen very often in web apps. The flow consists of using some request API (XHR, fetch, Axios), make a request to an URL we want to get some data from and it goes to the server to fetch it, then return it to us in a format we can understand and work with (JSON or XML but we almost always use JSON). It looks something like this visually 

![Networking in a nutshell (Image)](/media/img_0104.jpg "Networking in a nutshell ")

**\*Side note: JSON data looks like this -> {email: "janedoe@mail.com", password: "12345"} when you hear developers say they want the data back in JSON, it means like this. :)** 

### Different Request API's

Over the years, there have been many different API's to handle requests. XHR is the first one, then came the Fetch API, and lastly, you can see some people using Axios, which is an npm package that does most of the work for you. 

* XHR (AJAX)
* Fetch
* Axios (npm package)

### XHR (AJAX)

To make a request using the XHR Request API, we need to create an instance of the XHR request object.

```javascript
const xhr = new XMLHttpRequest();
xhr.onreadystatechange = () => {
  // if state of request is loading
  if (xhr.readyState === 3) {
    console.log("Loading...");
  }
  // if state of request is done
  if (xhr.readyState === 4) {
    xhr.status === 200
      ? console.log(xhr.responseText)
      : console.log("something went wrong");
  }
};
xhr.open("GET", "https://jsonplaceholder.typicode.com/todos");
xhr.send();
```

After we create an instance of the XHR request object. We check the state of the request in the \`\`\`onreadystatechange\`\`\` function using the \`\`\`readyState\`\`\` property. There are 4 states a request can be in  

**1: Opened (request starts)** 

**2: Headers received (http headers are received)** 

**3: Loading (response is loading/ downloading)**

**4: Done (the response is back)**

But here we're only checking for the loading state and done state. The \`\`\`status\`\`\` property specifies if the data came back or not. 200 means data came back good.

We call the \`\`\`open\`\`\` method and pass in which type of request method (in our case GET), second parameter specifies the URL we want data from (in our case https://jsonplaceholder.typicode.com/todos). This will give us dummy data of todo items. Lastly, we call the send() method to actually send the request out. 

**GET:** says we want to get data 

**POST:** says we want to send some data to the server 

**PUT:** says we want to update some existing data

**DELETE:** says we want to remove some data

## Fetch

Working with the Fetch API looks like this 

```javascript
// using the same URL 
fetch('https://jsonplaceholder.typicode.com/todos')
  .then(response => response.json())
  .then(json => console.log(json))
  .catch((err) => console.log("something went wrong:", err))
```

It does look much simpler than using the XHR request API. When making a simple GET request like this is simple to setup. In fetch requests, you need to specify that we want the response to be formatted in JSON (**response.json()**). Then, we can do whatever with that data afterward (in our case we **console.log()** ). The catch method handles any errors that occurs. 

Post request using Fetch

```javascript
const url = "https://someurl.com";
const data = { email: "johndoe@mail.com", password: "12345" };

fetch(url, {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data),
})
  .then((response) => {
    return response.json();
  })
  .then((data) => {
    console.log(data);
  }).catch((err) => {
    console.log('something went wrong:', err)
  })
```

With any post request you have to add more info about the data you're trying to send. The object passed after the url is the options to add more info. Here, we specify that it is a POST method (**method** property). Then, we need to let the server know what kind of data were sending up (**headers** property) by specify the "Content-Type" we set it to "application/json" which is basically JSON data. Lastly, we need to pass the actual data we want to send (**body** property). 

Strangely, the server can't read pure JSON data when we send it up, so we have to turn it to a string representation of the data. That's what **JSON.stringify(data)** does behind the scenes.

Lastly, we do like we did before and turn the response (data we get back) into JSON format. Then, we can do whatever. (we console.log it). This same process applies to doing PUT requests. 

## Axios (done with even more less code lol)

This is an npm package, therefore you need to install this from NPM

```javascript
import axios from 'axios'

axios.get('https://jsonplaceholder.typicode.com/todos/')
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.log(error);
  })
```

As you can see with axios you don't need to turn the response into JSON, it does that automatically behind the scenes. The data property (**response.data**) has the data we're looking for.

### Post request using axios

```javascript
axios.post('https://someurl.com', {
  method: 'post',
  data: {
    email: 'johndoe@mail.com',
    password: '12345'
  }
}).then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.log(error);
  })
```

Looks similar to the Fetch API post request. Everything is the same, it's just done differently.

Thats all folks. Enjoy :)