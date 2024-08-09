# Learning About Links

## Creating Links

Creating a link in an HTML document is straightforward. You need the an
anchor `<a> </a>` element, which needs an `href` attribute.

So the code would like like this:

```
<a href="url"> </a>
```

The value of the `href` attribute is the url you want to access.

The part of linking that takes the most effort is finding the correct link and using it correctly.

## Absolute vs. Relative

Remember when you were first learning about absolute and relative paths? The concept applies to links, relative and absolute urls.

### Absolute

Absolute paths are a way to access a document that starts at the root directory indicated by the forward slash at the start of the pathname (the notation we use to point to a specific file). The pathname is the route we take to access a document.

Absolute urls always include the protocol `https://` domain name and pathname, as necessary. The `htttps://` lets a computer know to look outside of the current server to find the url. Without it the browser looks at the current server to find the document (Robbins, 116). Absolute links are also called external links, because they take you to a location outside of the current site.

Here is an example of an external link:

```
    <ul>
      <li>The Food Network</li>
      <li><a href="https://www.epicurious.com/">Epicurious</a></li>
    </ul>
```

In the example above the absolute link points to epicurious.com.

Notice that I just typed out epicurious.com not https://www.epicurious.com/. This is because I am not creating a link element. When we type a url into our web browser search bar the browser knows that hypertext transfer protocol or hypertext transfer protocol secure (http or https) is implied and fills that part in for us.

---

### Relative

Relative urls are relative, meaning they are based on your current location on a. For example, I am on the about page of a website and want to link to the home page, I will create an anchor element (`<a href=""> </a>`) and the value of the `href` will be based on the about pages relationship to the home page.

![link from about page to home page](imgs/link_from_about_to_home.png)

In the image above we are on the about.html file. Line 45:

`<p><a href="index.html">Back to the home page</a></p>`

This code shows linking to the homepage (index.html). SWhen files are in the same directory the href value is the file name you want to link to. Because about.hml and index.html are in the same directory to get to index.html from about.html the href takes the value index.html.

A helpful analogy is a home address, 1234 SE Corgi Lane, Portland, OR 97206 United States of America. This address is always at this geographical location, absolute path. But, how someone gets there depends on their location.

When files aren't in the same directory the directions you give the browser to access the file is more involved. The pathname is still relative, but you live further away from 1234 Corgi Lane getting there will take more steps.

You can also write relative pathnames by starting with the root
directory and listing all the subdirectories until you get to where you want to be. This is called site root relative pathname. I often do this in the Linux command line. It helps me envision where I am going. The `/` at the start of a pathname indicates the root directory.

When you use the `/` you don't need to write the name of the root directory.

Because a site root relative pathname starts at the root to describe the pathname regardless of which subdirectory you are you will be able to access the linked document. Site root relative pathnames are useful for content than might not always be in the same directory or for dynamically generated material.

Unfortunately, site root relative pathnames won't work on your local device because they will be relative to your hard drive. You'll have to wait until the site is on the final server to check that these links work.

---

## Linking to a Lower Directory (Subdirectory)

Let's use the Jen's Test Kitchen examples from Learning Web Development's Chapter 6 to illustrate linking to files that are in separate folders.

For example we are on the index.html. We want to link the list item `<li>Tapenade (Olive Spread)</li>` to tapanade.html, which is in the recipes folder. All these files are in the JENSKITCHEN folder.

My first move is to add the anchor element to the list item:

`<li><a href="">Tapenade (Olive Spread)</a></li`

Next I look at where the index.html file lives. It is within the jenskitchen folder, it is not in another subfolder.

Now, I need to locate where the tapenade.html file is. As mentioned above it is in the recipes folder, which is subdirectory of jenskitchen. Making it nested within jenskitchen further making it a lower directory. So my approach to accessing it is to drill down.

So to access tapenade.html from index.html I need to:

1. Go to the recipes folder
2. When in the recipes folder click on the tapenade.html file.

The code would look like:

`li><a href="recipes/tapenade.html">Tapenade (Olive Spread)</a></li>`

The image below illustrates the file heriarchy in the left column. Line 48 shows where the anchor element was addded.

![link from index.html to tapenade.html](imgs/index_to_tapanade.png)

## Linking to a Higher Directory

There is a Looney Tunes image of a drill pushing above ground that illustrates linking to a higher directory. Essentially we are moving upwards until we make it to the directory we want.

The `../` tells us to go back one directory. You can string it together as many times as you need.

We want to create a link that takes us back to the homepage when we have linguine.html open. The linguine.html file is in the pasta directory, which is a subdirectory of the recipes directory. The recipes directory is a subdirectory of jenskitchen and index.html is located there.

From the pasta directory I need to drill up one to get to the recipe directory. So the path looks like this so far:

`../`

From recipes I need to drill up one more to get to jenskitchen. So the path looks like this now:

`../../`

Now I am in the folder that has index.html. So I just need to attach the file name to the end of the path:

`../../index.html`

That is the complete path.

The code:

`<p><a href="../../index.html">[Back to the home page]</a></p>`

![lingune.html to homepage](imgs/linguine_to_home.png)

---

## Linking to a Specific Point on a Page

Linking to a specific point on a page is a two step process.

### Identify the destination.

1. Ask yourself when I click on the link where will it go? Once you figure that out add an id attribute to the element you want to link to.

`<h2 id="section1">Section 1</h2>`

### Link to the Destination

2. Go to the element where you will click to get to the destination. Add the anchor tag to the element, and give the href the the value of the id attribute <a href="#section1"></a>

### Example

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Link to a Specific Point</title>
  </head>
  <body>
    <!-- Navigation Links -->
    <nav>
      <a href="#section1">Go to Section 1</a>
      <a href="#section2">Go to Section 2</a>
      <a href="#paragraph2">Go to Paragraph 2</a>
    </nav>

    <!-- Content Sections -->
    <h2 id="section1">Section 1</h2>
    <p>This is the content of section 1.</p>
  </body>
</html>
```

In this example, clicking "Go to Section 1" will take you to the `<h2> element with id="section1"`

The value following the # in a URL is called a fragment identifier or simply a fragment. The fragment identifier points to a specific section within a webpage.

You can link to a fragment within another document by adding the fragment name to the end of the url (works for both absolute and relative links).

1. `<a href="glossary.html#startH">See the Glossary, letter H</a>`

2. `<a href="http://www.example.com/glossary.html#startH">See the Glossary, letter H</a>`

---

## Opening Links in a New Window

Sometimes when you click on a link it will open in a new browser window. Wikipedia does this a lot. Robbins notes that opening links in a new browser can be confusing for some users and present accessibility issues for those using assistive technology. Another issue is that after clicking a link users may not come back to your content.

I didn't know about the accessibility issue. I hope to look into this more as I learn more about building accessible web technologies. I personally find links opening in new browser windows to be helpful. It is good to know that it isn't for everyone.

Adding the attribute `target` with a value of `_blank` to the anchor element will open a link in a new browser window.

`<a href="https://en.wikipedia.org/wiki/Labour_Party_(UK)" target="_blank">UK Labour Part</a>`

---

### Linking to an Email Address

Syntax:

`<a href=mailto:name@emailaddress.com></a>`

`<a href="omnia.abdul@protonmail.com>Contact Omnia</a>`

A browser has to be configured to launch a mail program. If you use an email as linked text it will work for everyone.

---

## Linking to a Telephone Number

Syntax:

`<a href="tel:+01-900-123-4567">Contact Us Today at (900) 123-4567!</a>`

Include the full international dialing number, that means include the country code. [A list of country codes.](https://www.countrycode.org/)

Also include the telephone number in the content of the link so if the link doesn't work people still know the number.

Androids and iPhones have a feature that detects phone numbers - automatically converting them to links. Some 10-digit numbers that are not phone numbers might be converted to links accidentally. If your document has strings of numbers that might be mistaken for a phone number you can turn off auto-detection by using this meta tag in the head portion of your document.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="format-detection" content="telephone=no" />
    <title>Jen's Kitchen</title>
  </head>
</html>
```
