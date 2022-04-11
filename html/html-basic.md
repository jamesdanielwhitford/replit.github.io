# HTML Basic Examples

First, let’s talk about the tools that we need to create an HTML file. The most important tool we need is an HTML editor. There are many choices on the market, but today we'll be using Replit. Replit allows us to easily create and HTML repl and host our website for free.   

To get started, [sign up](https://replit.com/signup) for a Replit account. One logged in, click `+ create` in the top left hand corner.


![Notepad UI Image](https://i.ibb.co/cccGq2t/Replit-HTML.jpg)

Type in `HTML` in the template field box and select the HTML,CSS, JS template. Then type in any title for your sample webpage. For this example, we have `"My Sample HTML Webpage"`. After that, click the `+ Create Repl` button.

Now, let's add content to your HTML file.

## Adding Content to our HTML Body

As mentioned above, we put our content inside the `<body>` tag. This includes text, images, tables, forms, and everything else we see on web pages.

**HTML Headings**

In HTML, headings are written in the following elements:

 - `<h1>This is the first heading</h1>`
   - `<h2>This is the second heading</h2>`
     - `<h3>This is the third heading</h3>`
       - `<h4>Fourth heading</h4>`
         - `<h5>Fifth heading</h5>`
            -  `<h6>Sixth heading</h6>`

As you may expect, `<h1>` and `<h2>` should be used for the most significant titles, while the remaining tags should be used for subheadings and less important information.

This order is used by search engine bots to determine which content on a page is most essential.

**HTML Paragraph**

HTML Paragraph is defined with a `<p>` tag:

    <p> This is a sample paragraph. </p>
    <p> This is another paragraph. </p>

**HTML Links**

To insert a link in HTML, we will use the `<a>` (or anchor) tag. 

    <a href="https://replit.com/"> Click here to proceed to Replit. </a>

The `href` points to the page that will open once the link is clicked.  

  **HTML Images**

To insert an image in HTML, we will use the `<img>` tag. 

     <img src="https://www.cp4l.org/images/replit_logo.png"  alt="Replit's Logo"  width="104"  height="142">

The source file (`src`), alternative text (`alt`), `width`, and `height` are attributes here in our `<img>` element.

# Create your own HTML File

In your notepad file, type in the following line of code:

    <html>
	    <head>
		    <title>Welcome! This is my webpage.</title>
	    </head>
	    <body>
		    <h1>This is the main heading</h1>
		    <h2>This is a subheading</h2>
			<p>This is a paragraph where I will discuss how I love HTML. </p>
			<a href="html.com"> Click here to learn more about HTML. </a>
			<br>
			<img src="https://w7.pngwing.com/pngs/201/90/png-transparent-logo-html-html5.png"  alt="HTML LOGO"  width="200"  height="200">
	    </body>
    </html>

Hit the `run` button on the upper center of your screen and you should see something like this:

![sample output](https://i.ibb.co/8zWqvVJ/Replit-HTML-2.jpg)

***Congratulations on your first HTML file!***

On our next topic, we will dive in further on different HTML tags, elements, and attributes.
 
To see the sample HTML site, you can visit [here](https://my-sample-html-webpage.pauleengregana.repl.co/).
