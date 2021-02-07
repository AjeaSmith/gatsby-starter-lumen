---
template: post
title: "Javascript In The Browser: The DOM (Nutshell)"
slug: js-in-browser-the-dom
socialImage: /media/javascript.png
draft: false
date: 2021-02-06T23:43:36.672Z
description: "Javascript In The Browser: The DOM (In a Nutshell)"
category: JS Nutshell
tags:
  - Javascript
  - DOM
  - coding
  - frontend
---
The DOM (Document Object Model) represents the structure of a webpage. It's an object that contains properties that describe the webpage.  

When you type "document" in the console, it shows you the outline of the webpage (the element tags that make up a webpage), e.g. (html, head, body, title, meta). (Image Below). It looks empty because we don't have any content yet.

![DOM outline (without content)](/media/domoutline.png "DOM Outline")

**\*Image below has some content that might look unfamiliar, I'll sum up briefly what they are meant for :)\***

**Body Tag:** The body tag is the most important because that's where our content needs to go for us to see it on our webpage

**Main, Header, Nav, Section, P, H1-H6:** These are typical tags you'll see **WITHIN** the body tag. These describe the different types of content you can have on your webpage. They're called Semantic Tags (you can [read more ](https://www.pluralsight.com/guides/semantic-html)about that and how it's good for SEO purposes)

**Classes:** (example: class="navbar" ) these are names you give the elements to reference them later, which makes it easier for us to modify it either in CSS or Javascript. 

![DOM Outline (with content)](/media/domwithcontent.png "DOM (with content)")

Now that we have some content on the page, let's modify some of it through Javascript (Since that's the main focus of this article). For us to start interacting with the DOM using Javascript we first need to create a JS file that we can work in and, then include that JS script inside our HTML file. Lastly, we'll find a way to grab our element tags from the DOM within our JS file. 

**1st: Include JS file in our Html file (I created an "main.js" file in root folder)**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Demo</title>
  </head>
  <body>
    ...
    <script src="main.js"></script>
  </body>
</html>
```

**2nd: Things get interesting as we find ways to grab element from DOM through JS.** 

**2 ways of doing this ->** 

1. **Using querySelectors ->** grab single DOM element by either classname or ID(we'll use classNames though) ex: 

```javascript
/* main.js */

// We're grabbing the (navbar, first article) element by the classnames 
// we assigned to them (we need to add . before the classname)

const navbar = document.querySelector(".navbar");
const firstArticle = document.querySelector(".article1");

// we should see those two elements in our console
console.log(navbar, firstArticle);
```

![(nav, section) element tags in the console](/media/console.png "(nav, section) element tags in the console")

2. **Traversing the DOM ->** this is helpful for when we need to access elements that are nested inside deeply, there are properties that will give us the next element based on the element were on (better shown then said lol) this way can be easier than grabbing one-by-one using querySelectors. 

```javascript
// Before, using querySelector 
// querySelectorAll(grabs multiple elements and stores it similar to arrays of li's)

const navbar = document.querySelector(".navbar");
const ul = document.querySelector(".navbar-menu");
const li = document.querySelectorAll("li");

console.log(li);

// Now, traversing the DOM
/* firstElementChild -> property to grab the child element of an element */
/* children -> property to grab the children of an element (in our case li's)*/
const navbar2 = document.querySelector(".navbar");
const ul2 = navbar.firstElementChild; 
const li2 = ul.children;

console.log(li2);
```

Thats just a taste of traversing the DOM, you can find more detailed info [here ](https://zellwk.com/blog/dom-traversals/)

Cool, we know how to grab elements both ways, (querySelector, traversing the DOM).

Lastly, let's modify it's content and style with Javascript

1. Using the **style** property(style is just another **object** that contains all the styles as properties) if you were to \`\`\`console.log(navbar.style)\`\`\` you would see this 

   ![](/media/styleprop.png)

   Back to the code :) we accessing the properties we want to change, and setting a value we want. Like how we would in a normal css file.

   ```javascript
   const navbar = document.querySelector(".navbar");
   const ul = navbar.firstElementChild;

   // changing the style of navbar using the *style* property
   navbar.style.backgroundColor = "pink";
   ul.style.listStyle = "none";
   ul.style.display = "flex";
   ul.style.padding = "1em";
   ul.style.justifyContent = "space-around";
   ul.style.fontWeight = "bold";
   ul.style.fontSize = "18px";

   ```

   Now, it looks like this after styling

   ![Styling the DOM with Javascript (style property)](/media/screen-shot-2021-02-06-at-9.23.23-pm.png "Styling the DOM with Javascript (style property)")

   2. Using the **add** method to style (we need to add a "style.css" file to say what classes we want to apply through JS) **\*Be sure to link up your stylesheet in your html file, as I always forget lol\***

   **GOAL: I want to style all 3 article element tags with the styles mentioned below**

   ```css
   /* Style.css file */

   /* This is the class styles we will apply using the addClass method*/
   .article-background-color {
     background-color: antiquewhite;
     color: rgb(101, 99, 99);
   }
   ```

   We grab all the article elements using the querySelectorAll method, however returns an HTML Collection**(line 1)** of elements and we cant loop through HTML Collections in JS. So, we convert them into arrays**(line 2)**, which we can loop through each one and access their **classList**(property), then use the add method to apply which styles from css we want **(.article-background-color) (line 4)**

   ```javascript
   const article = document.querySelectorAll(".article");
   const articleArray = Array.from(article);

   articleArray.forEach((el) => {
     el.classList.add("article-background-color");
   });

   ```

   The Final look using both styling approaches 

   ![Final look using both style approaches](/media/finalstyles.png "Final look using both style approaches")

   That's all for this one :) enjoy folks