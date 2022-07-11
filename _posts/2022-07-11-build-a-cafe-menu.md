---
title:  "Learn basic CSS by buidling a cafe menu"
excerpt: "CSS"

categories:
  - web
tags:
  - [CSS]

permalink: /css/build_a_cafe_menu/

toc: true
toc_sticky: true
 
date: 2022-07-11
last_modified_at: 2022-07-11
---

CSS (cascading style sheet)로 배경, 색깔, 폰트, 사이즈 등의 HTML element들을 조정할 수 있다. 

```html
<!-- file: index.html -->

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Cafe Menu</title>
    <!-- <style>
      h1, h2, p {
        text-align: center;
      }
    </style> -->
    <link rel="stylesheet" href="styles.css">
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />  <!--enables styling of the page to look similar on mobile as it does on a desktop or laptop -->
  </head>
  <body>
    <div class="menu">  <!-- enables application of the class's styling to div -->
    <header>
      <h1>CAMPER CAFE</h1>
      <p class="established">Est. 2020</p>
    </header>
    <hr>    <!-- used to display a divider -->
    <main>
      <section>
        <h2>Coffee</h2>
        <img src="https://cdn.freecodecamp.org/curriculum/css-cafe/coffee.jpg" alt="coffee icon">
        <article class="item">
          <p class="flavor">French Vanilla</p class="price"><p>3.00</p>
        </article>
        <article class="item">
          <p class="flavor">Caramel Macchiato</p><p class="price">3.75</p>
        </article>
        <article class="item">
          <p class="flavor">Pumpkin Spice</p><p class="price">3.50</p>
        </article>
        <article class="item">
          <p class="flavor">Hazelnut</p><p class="price">4.00</p>
        </article>
        <article class="item">
          <p class="flavor">Mocha</p><p class="price">4.50</p>
        </article>
      </section>

      <section>
        <h2>Desserts</h2>
        <img src="https://cdn.freecodecamp.org/curriculum/css-cafe/pie.jpg" alt="pie icon"/>
        <article class="item">
          <p class="dessert">Donut</p><p class="price">1.50</p>
        </article>
        <article class="item">
          <p class="dessert">Cherry Pie</p><p class="price">2.75</p>
        </article>
        <article class="item">
          <p class="dessert">Cheesecake</p><p class="price">3.00</p>
        </article>
        <article class="item">
          <p class="dessert">Cinnamon Roll</p><p class="price">2.50</p>
        </article>
      </section>
    </main>
    <hr class="bottom-line">
    <footer>
      <p>
        <a href="https://www.freecodecamp.org">Visit our website</a>
      </p>
      <p class="address">123 Free Code Camp Drive</p>
    </footer>
    <div>
  </body>
</html>
```

```css
/* file: styles.css */

h1, h2, p {
  text-align: center;
}

body {
  background-image: url(https://cdn.freecodecamp.org/curriculum/css-cafe/beans.jpg);
  font-family: sans-serif;
  padding: 20px;
}

h1, h2 {
  font-family: Impact, serif;  /* serif will be used if the first font (Impact) is not found/available. */
}

h1 {
  font-size: 40px;
  margin-top: 0;
  margin-bottom: 15px;
}
h2 {
  font-size: 30px;
}

hr {
  height: 2px;
  background-color: brown;
  border-color: brown;
}

img {
  display: block;
  margin-left: auto;
  margin-right: auto;
  margin-top: -25px;
}

.menu {  /* class selector */
  width: /*300px*/ 80%;
  background-color: burlywood;
  margin-left: auto;
  margin-right: auto;  /* center the div horizontally. */
  padding: 20px;
  max-width: 500px;
}

.item p {
    display: inline-block;
    margin-top: 5px;
    margin-bottom: 5px;
    font-size: 18px;
}

.flavor, .dessert {
    text-align: left;
    width: 75%;
}

.price {
    text-align: right;
    width: 25%;
}

.established {
    font-style: italic;
}

.bottom-line {
    margin-top: 25px;
}

.address {
    margin-bottom: 5px;
}


/* FOOTER */
footer {
    font-size: 14px;
}

a {
    color: black;    /* makes the footer link the same color regardless if a link has been visited */
}

/* pseudo-selectors */
a:visited {    /* change properties of a link when the link has been visited */
    color: black;
}

a:hover {    /* change properties of a link when the mouse hovers over them */
    color: brown;
}

a:active {    /* change properties of a link when the link is actually being clicked by. */
  color: brown;
}
```


Inside `head` element:
* `title`: provides extra information not visible on the web page. It is useful for search engines or how the page gets displayed.
* `<meta charset="utf-8>`: tell the browser how to encode characters for the page.
* `style`: used to add style to an element by setting a property for it like this: 
```html
element {
    property: value;
}
```
* `link` (self-closing tag).
  

`div`: used mainly for design layout purposes.


---
### CSS(Cascading Style Sheet)
CSS is a style sheet language used for describing the presentation of a document written in a markup language such as HTML.  
It is designed to enable the **separation of presentation and content**, including layout, colors, and fonts. This separation can:
* improve content accessibility.
* provide more flexibility and control in the specification of presentation characteristics.
* enable multiple web pages to share formatting by specifyint the relevant CSS in a separate .css file.
* enable the .css file to be cached to improve the page load speed between the pages that share the file and its formatting.


`article`: commonly contains **multiple elements** that have related information. 