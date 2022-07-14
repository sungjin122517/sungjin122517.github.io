---
title:  "Learn HTML forms by building a registration form"
excerpt: "HTML"

categories:
  - web
tags:
  - [HTML, form]

permalink: /web/build-registration-form/

toc: true
toc_sticky: true
 
date: 2022-07-14
last_modified_at: 2022-07-14
---





## Objective
Learn HTML forms by building a signup page.  
This form will collect information (name, email), create password, upload profile picture, etc.
    
    
![build-registration-form-1.png](/assets/images/posts_img/web/build-registration-form-1.png)
![build-registration-form-2.png](/assets/images/posts_img/web/build-registration-form-2.png)
    
    
---


```html
<!DOCTYPE html>
<html>
  <head>
    <title>Registration Form</title>
	<link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <h1>Registration Form</h1>
    <p>Please fill out this form with the required information</p>
    <form action="https://register-demo.freecodecamp.org">
      <fieldset>    <!-- first section -->
        <label>
          Enter Your First Name: <input type="text" required name="first-name">
          <!-- default of type attribute: text -->
        </label>
        <label>
          Enter Your Last Name: <input type="text" required name="last-name">
        </label>
        <label>
          Enter Your Email: <input type="email" required name="email">
        </label>
        <label>
          Create a New Password: <input type="password" pattern="[a-z0-5]{8, }" required name="pw">
        </label>
      </fieldset>    

      <fieldset>    <!-- second section -->
        <label><input type="radio" name="account-type" class="inline"/> Personal Account</label>
        <label><input type="radio" name="account-type" class="inline"/> Business Account</label>
        <label><input type="checkbox" required class="inline"/> I accept the <a href="https://www.freecodecamp.org/news/terms-of-service/">terms and conditions</a></label>
      </fieldset>    

      <fieldset>    <!-- thrid section: allow users to upload profile picture -->
        <label>Upload a profile picture: <input type="file" name="profile-pic"></label>
        <label>Input your age (years): <input type="number" min="13" max="120" name="age"></label>
        <label>How did you hear about us?
          <select name="referrel">
            <option value="">(select one)</option>
            <!-- Without value attribute in option, submitting the form with the option would not send a useful value to the server. -->
            <option value=1>freeCodeCamp News</option>
            <option value=2>freeCodeCamp YouTube Channel</option>
            <option value=3>freeCodeCamp Forum</option>
            <option value=4>Other</option>
          </select>
        </label>
        <label>
          Provide a bio:
          <textarea rows="3" cols="30" placeholder="I like coding on the beach..." name="bio"></textarea>    <!-- placeholder attribute accepts a text value which is displayed until the user starts typing. -->
        </label>
      </fieldset>
      <input type="submit" value="Submit">    <!-- automatically set to submit its nearest parent form element. -->
    </form>
  </body>
```


```css
body {
  width: 100%;
  height: 100vh;
  margin: 0;    /* by setting margin to 0, horizontal scroll-bar is removed. */
  background-color: #1b1b32;
  color: #f5f6f7;    /* text color */
  font-family: Tahoma;
  font-size: 16px
}

label {
  display: block;    /* make label elements appear on separate lines (label elements are inline by default). */
  margin: 0.5rem 0;    /* enables spacing between lines */
}

h1, p {
  margin: 1em auto;
  text-align: center;
}

form {
  margin: 0 auto;
  max-width: 500px;
  min-width: 300px;
  width: 60vw;
  padding-bottom: 2em;
}

fieldset {
  /* padding-top: 2rem;
  padding-bottom: 2rem;
  padding-left: 0;
  padding-right: 0; */
  padding: 2rem 0;
  border: none;    /* removes default border */
  border-bottom: 3px solid #3b3b4f;
}

/* This targets the last fieldset element and sets a change. */
fieldset:last-of-type {border-bottom: none;}

input, textarea, select {
  width: 100%;    /* makes label text appear above the form elements. */
  margin-top: 10px;
  margin-bottom: 0;
  margin-left: 0;
  margin-right: 0;
  min-height: 2em;
}

input, textarea {
  background-color: #0a0a23;
  border: 1px solid #0a0a23;
  color: #ffffff;
}


/* attribute selector: selects an element based on the given attribute value. */
input[type="submit"] {
  display: block;
  width: 60%;
  margin: 1em auto;    /* aligns the button at the center */
  height: 2em;
  font-size: 1.1rem;
  background-color: #3b3b4f;
  border-color: white;
  min-width: 300px;
}

input[type="file"] {
  padding: 1px 2px;
}

a {
  color: #dfdfe2;
}


/* class selectors */
.inline {
  width: unset;    /* removes the earlier rule that set all the input elements to width: 100%. */
  margin-right: 0.5em;
  margin-left: 0;
  margin-top: 0;
  margin-bottom: 0;
  vertical-align: middle;
}
```

---
Attributes inside `input` element:
* `required`: enables error message to appear if you try to submit the form without filling in the required fields.
* `minlength`: custom validation prevents inputs of less than 8 characters being submitted.
* `pattern`: define a regular expression that the password must match to be considered valid.  
  e.g. `pattern="[a-z0-5]{8, }"`: matches eight or more lowecase letters or the digits 0 to 5. 
      
    
`select`: adds a **dropdown** to the form. It is a container for a group of `option` elements, which acts as a label for each dropdown option.

`textarea`: acts like an `input` element of type `text`, but comes with the added benefit of being able to :
1. receive multi-line text, and
2. set initial number of text rows and columns.
    
    
With form submissions, it is useful to provide each submittable element with a `name` attribute, which is used to identify the element in the form submission.

