---
title:  "Learn HTML by buidling a cat photo app"
excerpt: "HTML"

categories:
  - web
tags:
  - [HTML]

permalink: /html/build_cat_photo_app/

toc: true
toc_sticky: true
 
date: 2022-07-07
last_modified_at: 2022-07-07
---

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>CatPhotoApp</title>
  </head>
  <body>
    <h1>CatPhotoApp</h1>
    <main>
      <section>
        <h2>Cat Photos</h2>
        <!-- TODO: Add link to cat photos -->
        <p>Click here to view more <a target="_blank" href='https://freecatphotoapp.com'>cat photos</a>.</p>
        <!-- <a href='https://freecatphotoapp.com'>cat photos</a> -->
        <a href="https://freecatphotoapp.com"><img src="https://cdn.freecodecamp.org/curriculum/cat-photo-app/relaxing-cat.jpg" alt="A cute orange cat lying on its back."></a>
      </section>

      <section>
        <h2>Cat Lists</h2>
        <h3>Things cats love:</h3>
        <ul>
          <li>cat nip</li>
          <li>laser pointers</li>
          <li>lasagna</li>
        </ul>
        <figure>
          <img src="https://cdn.freecodecamp.org/curriculum/cat-photo-app/lasagna.jpg" alt="A slice of lasagna on a plate.">
          <figcaption>Cats <em>love</em> lasagna.</figcaption>
        </figure>
        <h3>Top 3 things cats hate:</h3>
        <ol>
          <li>flea treatment</li>
          <li>thunder</li>
          <li>other cats</li>
        </ol>
        <figure>
          <img src="https://cdn.freecodecamp.org/curriculum/cat-photo-app/cats.jpg" alt="Five cats looking around a field.">
          <figcaption>Cats <strong>hate</strong> other cats.</figcaption>  
        </figure>
      </section>

      <section>
        <h2>Cat Form</h2>
        <form action="https://freecatphotoapp.com/submit-cat-photo">
          <fieldset>
            <legend>Is your cat an indoor or outdoor cat?</legend>
            <label><input id="indoor" type="radio" name="indoor-outdoor" value="indoor" checked> Indoor</label>
            <label><input id="outdoor" type="radio" name="indoor-outdoor" value="outdoor"> Outdoor</label>
          </fieldset>

          <fieldset>
            <legend>What's your cat's personality?</legend>
            <input id="loving" type="checkbox" name="personality" value="loving" checked> <label for="loving">Loving</label>
            <input id="lazy" type="checkbox" name="personality" value="lazy"> <label for="lazy">Lazy</label>
            <input id="energetic" type="checkbox" name="personality" value="energetic"> <label for="energetic">Energetic</label>
          </fieldset>

          <input type="text" name="catphotourl" placeholder="cat photo URL" required>
          <button type="submit">Submit</button>
        </form>
      </section>    
    </main>
    <footer>
      <p>
      No Copyright - <a href="https://www.freecodecamp.org">freeCodeCamp.org</a>
      </p>
    </footer>
  </body>
</html>
```


`h1` to `h6`: Heading elements. Lower the number, highter the importance.  
`p`: used to create a paragraph of text.  
`<!--` to `-->`: comment

HTML5 has some elements that identify different content areas, e.g. `main`.

`img`: add images. It has **no closing tag**, therefore called `self-closing tag`.

HTML `attributes`: special words **used inside the opening tag of an element** to control the element's behaviour.
* `src`: speficies the image's URL.
* `alt`: displayed if the image fails to load.
* `action`: used inside `form` element. Indicates where form data should be sent. 

anchor(`a`): enables link to another page.  
`target="_blank"`: enables link to be opened in a new tab.

`ul`: unordered list (bullet point.)  
`ol`: ordered list (its list items are numbered when displayed.)  
`li`: list item.

`figure`: represents self-contained content and will allow you to associate an image with a caption.  
`figcaption`: add a caption to describe the image contained within the `figure` element.  
`em`: emphasize the word (**italic**).  
`strong`: indicate strong importance/urgent (**bold**).

`form`: collect information from users.  
`input`: `self-closing tag`. Allows you several ways to collect data from a web form.  

`attributes` used inside `input` element:
* `type`
* `name`: a value to represent the submitted data is assigned to it. Same `name` value should be added to both radio buttons to make sure selecting one radio button automatically **deselects** the other.
* `placeholder`: give people a hint about what kind of information to enter into an input.
* `required`: prevent a user from submitting your form when required information is missing. **No value is set to it**.
* `id`: identify specific HTML elements.
* `value` (optional)
* `checked`: make a checkbox checked or radio button selected **by default**. No value is set to it.

`button`: create a clickable button. The **default behaviour** of clicking a form button without any attributes submits the form to the location specified in the form's `action` attribute.  
`radio` button: used for questions where you want **only one answer** out of multiple options.  
`label`: associate the text for an `input` element with the input element itself. From the example above, clicking the word `Indoor`  also selects the corresponding radio button.  
`fieldset`: group related inputs and labels together in a web form. It is a **block-level** element, meaning that it appears on a new line.  
`legend`: acts as a caption for the content in the `fieldset` element.

Inside `head` element:
* `title`: determines what browsers show in the title bar or tab for the page.

`!DOCTYPE html`: ensures the browser tries to meet industry-wide specifications (업계 표준/규격).
