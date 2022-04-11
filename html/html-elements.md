# HTML ELEMENTS

An HTML Element is an individual component of an HTML document. It represents the semantics or meaning. It usually contains three parts: the opening tag, the content, and the closing tag. 

Below is an example of an HTML element. 

` <p> This is a sample paragraph. </p> `

- The `<p>` is the opening tag which defines that this HTML element is a paragraph. 
- The `This is a sample paragraph` is the content. 
- The `</p>` is the closing tag which denotes the end of the paragraph element. 

## Empty HTML Elements

Not all HTML elements have a content and a closing tag. This type of HTML element is called `empty elements` or `self-closing elements`. 

A common example of an empty element is the <br> element which is used for a line break. Other common empty elements are `<img>`, `<link>`, `<input>`, `<meta>`, `<hr>` and many more.

Below is an example of HTML code using empty elements.

> `<p> This is a paragraph written in <br> two lines </p>`
> 
> `<img src =”images/sky.jpg”>`
> 
> `<input type=”text” name=”Input your name: ”>`

## Nested HTML Elements

HTML elements can contain other elements. Placing an element inside another is called nesting. A `nested element` is called a `child element`. An HTML child element can be referred to as parent element too if other elements are nested inside.

The next example shows other HTML elements nested inside our `<p>` element.

> ` <p> This sentence contains <b> <i> bold  and italized </i> </b> words </p>`

Take note that HTML nested elements should be closed in the correct order. They must be closed in the inverse order of how they were written, that means the last tag opened must be closed first.

## Don’t Skip the Closing tag

Some HTML elements will display correctly even if you will not put the closing tag. 

> `<p> This is a paragraph`
> 
> `<p> This is another paragraph `

However, this is not recommended because unexpected results or errors may occur. So, never skip the closing tag!

## HTML Case Insensitivity

HTML tags are **not case sensitive**. It means the `<P>` tag and the `<p>` tag are just the same paragraph tag in HTML. 

However, using lowercase is recommended for both HTML tags and attributes. Typing HTML tags in lowercase will make your document more compliant for future upgrades. 
 
## HTML Elements Type

HTML elements can be categorized into two: `block level` and `inline level` elements:

- **Block-level elements** - these are elements that make up the webpage’s structure. It occupies 100% available width. These elements are automatically rendered with a line break before and after. The most commonly used block-level elements are `<div>`, `<h1>` to `<h6>`, `<p>`, `<form>`, `<ol>`, `<ul>`, `<li>`, and many more.
 
- **Inline-level elements** - these are elements contained inside the block-level elements. Inline-level elements will take up the space that it only needs. Th most commonly used elements for this type of element are: `<a>`, `<strong>`, `<span>`, `<b>`, `<i>`, `<input>`, `<button>`, etc.

Throughout this entire course, you will encounter more of these HTML elements.  

# HTML Example

Using the Replit editor, let's now create our HTML page using the concepts that we have learned today. 

If you haven't used Replit before, you can [sign up](https://replit.com/signup) here. One logged in, click `+ create` in the top left hand corner and select the `HTML,CSS, JS` repl template. From there, write the code below into the html file. 

```
<html>
    <head>
        <title> HTML Elements </title>
    </head>
    <body>
        <h1> I am excited to learn more about HTML Elements. </h1>
        <b><i><u> This is a sentence with bold, italic, and underline elements. </u> </i> </b>
        <ol> Please type in your name here: <input type=”text” name=”firstname”> </ol>
<strong> See you on our next discussion! </strong>
    </body>
</html>
```

Hit the `run` button on the upper center of your screen and you should see something like this:

![sample output](https://i.ibb.co/R9kWmZp/Screenshot-20220402-151109-Chrome.jpg)
