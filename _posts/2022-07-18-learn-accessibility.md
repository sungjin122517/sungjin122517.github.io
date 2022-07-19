---
title:  "Learn accessibility by building a quiz"
excerpt: "learn accessibility tools: keyboard shortcuts, ARIA attributes"

categories:
  - web
tags:
  - [html, css, keyboard shortcuts, ARIA attributes]

permalink: /web/learn_accessibility_tools/

toc: true
toc_sticky: true
 
date: 2022-07-18
last_modified_at: 2022-07-18
---

![build-quiz-form.png](/assets/images/posts_img/web/build-quiz-form.png)

<br>

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" content="freeCodeCamp Accessibility Quiz practice project" />
    <title>Accessibility Quiz</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <header>
      <img id="logo" src="https://cdn.freecodecamp.org/platform/universal/fcc_primary.svg">
      <h1>HTML/CSS Quiz</h1>
      <nav>
        <ul>
          <!-- href enables to be able to navigate within the page -->
          <li><a href="#student-info" accesskey="s">INFO</a></li>
          <li><a href="#html-questions" accesskey="h">HTML</a></li>
          <li><a href="#css-questions" accesskey="c">CSS</a></li>
		    </ul>
      </nav>
    </header>
    <main>
      <form method="post" action="https://freecodecamp.org/practice-project/accessibility-quiz">
        <section role="region" aria-labelledby="student-info">
          <h2 id="student-info">Student Info</h2>
          <div class="info">
            <label for="student-name">Name:</label>
            <input id="student-name" type="text" name="student-name" placeholder="e.g. SUNG, Jin"/>
          </div>
          <div class="info">
            <label for="student-email">Email:</label>
            <input id="student-email" type="email" name="student-email"/>
          </div>
          <div class="info">
            <label for="birth-date">
              D.O.B.:<span class="sr-only">(Date of Birth)</span>
            </label>
            <input id="birth-date" type="date" name="birth-date"/>
          </div>
        </section>
        <section role="region" aria-labelledby="html-questions">
          <h2 id="html-questions">HTML</h2>
          <div class="question-block">
            <p>1</p>
            <fieldset class="question" name="html-question-one">
              <legend>
                The legend element represents a caption for the content of its
                parent fieldset element
              </legend>
              <ul class="answers-list">
                <li>
                  <label for="true-1">
                    <input type="radio" id="true-1" value="True" name="true-false-1"/>
                  </label>
                </li>
                <li>
                  <label for="false-1">
                    <input type="radio" id="false-1" value="False" name="true-false-1"/>
                  </label>
                </li>
              </ul>
            </fieldset>
          </div>
          <div class="question-block">
            <p>2</p>
            <fieldset class="question" name="html-question-two">
              <legend>
                A label element nesting an input element is required to have a
                for attribute with the same value as the input's id
              </legend>
              <ul class="answers-list">
                <li>
                  <label for="true-2">
                    <input type="radio" id="true-2" value="True" name="true-false-2"/>
                  </label>
                </li>
                <li>
                  <label for="false-2">
                    <input type="radio" id="false-2" value="False" name="true-false-2"/>
                  </label>
                </li>
              </ul>
            </fieldset>
          </div>
        </section>
        <section role="region" aria-labelledby="css-questions">
          <h2 id="css-questions">CSS</h2>
          <div class="formrow">
            <div class="question-block">
              <label for="customer">Are you a frontend developer?</label>
            </div>
            <div class="answer">
              <select required name="customer" id="customer">
                <option value="">Select an option</option>
                <option value="yes">Yes</option>
                <option value="no">No</option>
              </select>
            </div>
            <div class="question-block">
              <label for="css-questions">Do you have any questions:</label>
            </div>
            <div class="answer">
              <textarea rows="5" cols="24" placeholder="Who is flexbox..." id="css-questions" name="css-questions"></textarea>
            </div>
        </section>
        <button type="submit">Submit</button>
      </form>
    </main>
    <!-- footer and address -->
    <footer>
      <address>
        <a href="https://freecodecamp.org">freeCodeCamp</a><br />
        San Francisco<br />
        California<br />
        USA
      </address>
    <footer>
  </body>
</html>
```

#### Elements under head
`meta`: **element** used to specify information about the page, such as the title, description, keywords, and author.  
`charset`: **attribute** that specifies the character encoding of the page.  
`viewport`: `viewport` **definition** tells the browser how to render the page, by improving SEO (search engine optimization) and visual accessibility on mobile.  
`description`: `description` **definition** provides a brief summary of a web page. The sentences under `content` attribute is displayed as part of the search snippet in a search engine results page (SERP) and is meant to give the user an idea of the content within the page and how it relates to their search query.


It is important to <mark>link each `input` to the corresponding `label` element</mark>. This is done by giving the `label` a `for` attribute, which contains the `id` of the `input`.

<br>

#### Elements under body
`header`: **element** used to introduce the page and provide a navigation menu.  
Within the header:
* `img`
* `h1`
* `nav`


`main`: **element** that contains the core content of the page.

<br>

---





```css
@media (prefers-reduced-motion: no-preference) {
  * {    /* all */
    scroll-behavior: smooth;
  }
}

body {
	background: #f5f6f7;
	color: #1b1b32;
	font-family: Helvetica;
	margin: 0;
}

#logo {    /* using id as selector */
    width: max(100px, 18vw);
}

header {
	width: 100%;
	height: 50px;
	background-color: #1b1b32;
	display: flex;
	justify-content: space-between;    /* put horizontal space between the children <li> */
	align-items: center;    /* vertically center the children <li> */
	position: fixed;
	top: 0; 
}

h1 {
    color: #f1be32;
    font-size: min(5vw, 1.2em);
}

nav > ul {    /* targets <ul> within <nav> */
    display: flex;
    justify-content: space-evenly;
    /* uses Flexbox to evenly space the children */
    flex-wrap: wrap;
    align-items: center;
    padding-inline-start: 0;
    margin-block: 0;
    height: 100%;
}

h1, h2 {
	font-family: Verdana, Tahoma;
}

h2 {
	border-bottom: 4px solid #dfdfe2;
  /* replace top margin with 60px of top padding */
  margin-top: 0;
  padding-top: 60px;
}

p::before {   
  content: "Question #";
}

nav > ul > li {
	color: #dfdfe2;
	margin: 0 0.2rem;
	padding: 0.2rem;
	display: block;
}

li > a {
  color: #dfdfe2;
  text-decoration: none;    /* remove the underline from the anchor tags */
}

nav > ul > li:hover {    /* when the cursor hovers over the list elements, the background color and text color are switched to the colors below, and the cursor becomes a pointer */
	background-color: #dfdfe2;
	color: #1b1b32;
	cursor: pointer;
}

section {
	width: 80%;
	margin: 10px auto;    /* align section elements at the center */
	margin-top: 0;
	max-width: 600px;
}

input {
  font-size: 16px;
}

p {
  margin-top: 5px;
  padding-left: 15px;
  font-size: 20px;
}

footer {
  background-color: #2a2a40;
  display: flex;
  justify-content: center;    /* horizontally center the text */
}

footer, footer a {
  color: #dfdfe2;
}

address {
  text-align: center;
  padding: 0.3em;
}

.sr-only {    /* visually hide text for only screen readers to read */
	position: absolute;
	width: 1px;
	height: 1px;
	padding: 0;
	margin: -1px;
	overflow: hidden;
	clip: rect(0, 0, 0, 0);
	white-space: nowrap;
	border: 0;
}

.info {
  /* top bottom right left */
  padding: 10px 0 0 5px;
}

.formrow {
  margin-top: 30px;
	padding: 0px 15px;
}

.info > input {    /* target only the input elements within .info elements */
  width: 50%;
  text-align: left;
}

.info > label, .info > input {
  display: inline-block;    /* align the input boxes */
  text-align: right;    /* align text to the right */
}

.question {
  border: none;
  padding-bottom: 0;
}

.answers-list {
  list-style: none;    /* remove default styling for the list items (<li>->number in this case) */
  padding: 0;
}
```

`p::before`: `before` pseudo-element is used to prevent unnecessary repetition.

