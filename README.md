# FEDev-practical-sample-stage-4

NOTE: A Captioned video work through of this stage has been published at:
- (coming soon)

This document summarises the steps I took when creating my solution to the sample FEDev Practial 1

The stages of development required are:
```
Stage 1. Basic HTML structure for 2 pages: “index.html” and “characters.html”
   a. No CSS
   b. No links
   c. No images

Stage 2. Add images

Stage 3. Add nav links

Stage 4. Add CSS, to make the pages look like the provided screenshots
   a. Using CSS style rules in 1 or more “.css” files

Stage 5. Refactor the website as a Svelte(kit) project
   a. Demonstrate reusable Svelte components, such as:
       i. Nav bar
       ii. page footer

Stage 6. Add a third “merchandise” page
   a. Add a link to this page in the nav bar
   b. Style this in a similar style to the other 2 pages
   c. Find images from the web for several merchandise items
   d. Add a form at the bottom of this page asking for:
       i. Name / email address / postal address
       ii. (you do NOT have to write code to process this forms submission)

Stage 7. For an ‘A’ grade illustrate some/all of the following:
   a. Replacing standard CSS rules with TailWindCSS
   b. Populating the merchandise page contents by looping through JSON data
   (rather than hard coded page content)
   c. Publish the site as static pages via GitHub Actions
```

Stage 4. Add CSS, to make the pages look like the provided screenshots

There is a lot in this step, I suggest you approach this by:
- working one 1 page at a time (home page is simplest, so start with that)
- working on one aspect of the page at a time

It's useful to look carefully at the screenshot of the target website and make notes about the stylistic elememts. Here are a few aspects of the home page identified in this annotated screenshot:

![annotated screenshot of home page](/screenshots/index_page_annotated.png)

1. let's create a main CSS file for the project `/css/main.css`. I usually add a body background colour rule, to make it obvious that the CSS stylesheet is being read and applied by the browser:

   ```html
    body {
        background-color: beige;
    }
    ```

1. While we are at it, we'll make all text default to white:

    ```html
    body {
        background-color: beige;
        color: white;
    }
    ```

1. Inspecting the image carefully, the background colour from the screenshots seems to be ` #a07a21`. This colour will 'tint' the background image nicely:

    ```html
       body {
        background-color: beige;
        color: a07a21;
    }
    ```

1. Then in the `<head>` of each page we need to add a `<link>` element, so the styles rules in the CSS file are loaded an applied to the HTML elements of the page:

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <title>Rings of power - home page</title>
        <link rel="stylesheet" href="/css/main.css">
    </head>
    ```

1. let's center the header, and make its image 40% of page width. Add the follow CSS rule:
   
   ```html
   header {
      text-align: center;
      padding-bottom: 1rem;
   }
   
   header img {
       width: 40%;
   }
   ```




1. let's make the splash image, inside `<main>` have a width the full width of the web browser window, i.e. 100%:

   ```html
   main img {
       width: 100%;
   }
   ```


1. For the footer, let's center text (and images):

   ```html
   footer {
       text-align: center;
   }
   ```

1. make the width of the Prime logo image in the footer 5% of the available width:

   ```html
   footer img{
       width: 5%;
   }
   ```

1. We need to add a background image. Background images typical cover the whole page (`background-size: cover`), do not repeat, and are fixed (no scrolling):

   ```html
   body {
       background: url("/images/background.png") no-repeat center center fixed;
       background-size: cover;
   
       background-color: #a07a21;
       color: white;
   }
   ```

NOTE: The background color needs to appear AFTER the background image, otherwise it will be covered up by the background image


1. Now let's look at an annotated version of the characters page, to identify style features:


![annotated screenshot of characters page](/screenshots/characters_page_annotated.png)

1. Let's create a basic 4-column layout, with rows that use `display:flex` and columns taking up 25%.

   ```html
   .row {
       display: flex;
   }
   
   .col4 {
       width: 25%;
   }
   ```

1. We can add some padding to the rows and columns, and default text to be fully justified:

   ```html
   .row {
       padding: 0.5rem;
       display: flex;
   }
   
   .col4 {
       width: 25%;
       padding: 0.2rem;
       text-align: justify;
   }
   ```

1. for the rows and columns to work, we need to add `<div>`s with appropriate classes around our characters text and image content.
   - we also need to arrange the text and images into appropriately ordered columns
   - for example, Galadriel text first, then image, then Halbrand image, then text, and so on ...
   
   ```html
   <main>
   
       <div class="row">
           <div class="col4">
               <h3>
                   GALADRIEL
               </h3>
               <p>
   
                   Galadriel, an Elf is a key part of the story. We meet her in the Lord of the Rings, when she
                   welcomes the Fellowship to Lothlórien. In The Rings of Power, we meet a younger Galadriel who
                   is a very different Galadriel: a fierce warrior who we meet on a mission to find Sauron after her
                   brother died at his hands.
               </p>
           </div>
   
           <div class="col4">
               <img src="images/galadriel.jpg" alt="galadriel.jpg">
           </div>
   
           <div class="col4">
               <img src="images/halbrand.jpg" alt="halbrand.jpg" >
           </div>
   
           <div class="col4">
               <h3>
               HALBRAND
               </h3>
               <p>After abandoning her ship to continue her mission to locate Sauron, she’s left adrift in the
               Sundering Seas before a broken boat full of humans rescue her. Among them is Halbrand who
               develops an uneasy alliance with Galadriel as the pair begin their journey to the island of
               Numenor.
               </p>
           </div>
       </div>
   
   
       <div class="row">
           <div class="col4">
               .. and so on
   </main>
   ```

1. We can add the elegent left- and right- rounded borders as follows, with appropriate CSS class names:

   ```html
   .rounded_left {
       border-radius: 20% 0 0 20%;
   }
   
   
   .rounded_right {
       border-radius: 0 20% 20% 0;
   }
   ```

1. We can then add these class names to the appropriate HTML elements, for the style to be applied
   - for example, here we make the image for Galadriel have rounded right border
   - but for Halbrand we make the border rounded left
   
   ```html
       <div class="row">
           <div class="col4">
               <h3>
                   GALADRIEL
               </h3>
               <p>
   
                   Galadriel, an Elf is a key part of the story. We meet her in the Lord of the Rings, when she
                   welcomes the Fellowship to Lothlórien. In The Rings of Power, we meet a younger Galadriel who
                   is a very different Galadriel: a fierce warrior who we meet on a mission to find Sauron after her
                   brother died at his hands.
               </p>
           </div>
   
           <div class="col4">
               <img src="images/galadriel.jpg" alt="galadriel.jpg" class="rounded_right">
           </div>
   
           <div class="col4">
               <img src="images/halbrand.jpg" alt="halbrand.jpg" class="rounded_left">
           </div>
   
           <div class="col4">
               <h3>
                   HALBRAND
               </h3>
               <p>After abandoning her ship to continue her mission to locate Sauron, she’s left adrift in the
                   Sundering Seas before a broken boat full of humans rescue her. Among them is Halbrand who
                   develops an uneasy alliance with Galadriel as the pair begin their journey to the island of
                   Numenor.
               </p>
           </div>
       </div>
   ```

1. Let's increase the letter spacing for the character heading text:
   
   ```html
   .col4 h3 {
       letter-spacing: 0.4rem;
   }
   ```

1. We can also add some padding, and set the font-size to be proportiuonal to the XX for both the character headings and text:

   ````html
   .col4 p, .col4 h3 {
       padding: 0 1.5rem;
       font-size: 1cqw;
   }
   ````

## Styling the navigation bar

1. it's common to put the navigation styling into its own CSS file, so create file `/css/nav.css`, and add a link to this stylesheet for both your HTML pages

1. let's style our `nav` element to display `flex`, so blocks can be arranged horizontally, left-to-right. We'll also add some margin spacing below the nav bar, and set its background to black:

   ```html
   nav {
       display: flex;
   
       background-color: black;
       margin-bottom: 1rem;
   }
   ```

1. since we're using an unordered list for our navigation, we need to remove the bullet points (`list-style-type`). We'll also add an `auto` horizonal margin, so flex (list item blocks) content is centered:

   ```html
   nav ul {
       list-style-type: none;
       margin: 0 auto;
       padding: 1rem;
   }
   ```

1. we'll allow our list items to behave as inline elements:
   
   ```html
   nav ul li {
       display: inline;
   }
   ```

1. for our nav link elements (`<a>`), we'll remove the default underline (`text-decoration: none`), set the color to a nice gold color. We'll center the links, make them wide (so HOME is as wide as CHARCTERS), and add a little padding):

   ```html
   nav a {
       text-decoration: none;
       color: gold;
       text-align: center;
       width: 10rem;
       padding: 1rem;
   }
   ```

1. we can add the rollover image when the mouse hovers over a link. Using `background-size: cover` the image will fit the size of the link box being rolled over:

   ```html
   nav a:hover {
       background: url("/images/hover.png") center center;
       background-size: cover;
   }
   ```

1. finesse - you could change the link colours to a nicer gold
   - also you could add nice Google fonts perhaps ...


   ```html
   nav a {
       color: #9e8545;
        ...
   }
   ```
