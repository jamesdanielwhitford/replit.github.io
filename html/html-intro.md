
# Introduction to HTML

## What is HTML? 
HTML stands for HyperText Markup Language where HyperText stands for the link between web pages while Markup Language means the text between tags that define the structure. HTML is a basic hypertext markup language that is easy for humans to write and easy for computers to read. It is used to create web pages and define the structure of the web page.

## HTML Tags

The core of the HTML is the **tag**. Tags tells a web browser about the web page or something inside the page. HTML tags begin with less-than symbol **(<)** and end with the greater-than symbol **(>)**. It should look like this:

> `<html>`

## HTML Elements

HTML elements are the building blocks of a web page. They are created using tags. An HTML element is defined by an HTML opening tag, content, and an HTML closing tag. Let's breakdown this example below. 

> `<p color=”red”> This is our first paragraph. </p>`

 - `<p>` is the opening tag that is used to state where an element starts to take effect.
 - `color="red"` is an attribute which composes of two sections – a *name* and *attribute* value. The name identifies the additional information that a user wants to add, while the attribute value gives further specification.
 - `This is our first paragraph` is the content users see.
 - `</p>` is the closing tag which is used to state where an element will
   end.

Note that some of the HTML elements have no content and do not need a closing tag. These HTML elements are called *empty elements* or *self-closing tags*. One example of the empty element is the `<br>` which is used to break a line.

## HTML Skeleton

Consider the human body: we perceive skin, hair, arms, and legs when we look at someone. The skeleton underneath keeps us together and makes our body parts intact. The web page we see in a browser is like our body,  well-designed and appealing to the eye. The backbone of a web page is the HTML elements, which hold it all together and ensures that it looks good. The basic skeleton every of web page looks like this:

    <!DOCTYPE html>
    <html>
	    <head>
		    <title> Title of the web page </title>
	    </head>
	    <body>
	    </body>
    </html>

 - The `<!DOCTYPE html>` tells the browser what version HTML the document is written in. 
 - The `<html>` tag tells web browsers that the document is an HTML file.
 - The `<head>` tag holds the meta information about the web page.
 - The `<title>` tag reflects the description of a web page (like a title of a book that reflects its content). The content inside this tag will appear in the title bar of your web browser.
 - The `<body>` tag contains all the visible content of the web page.

To make your HTML code readable to humans, it’s essential that we use white space, new lines, spaces, and proper indentation.

*Note: When several tags are used, they must be closed in the order in which they were opened. For example:*

> `<b> <i> This is a bold and italicized text. </i> <b>`

You will learn more about HTML elements on our next topic. If you're interested, here is also a brief timeline of HTML.

## HTML History

-   **1991-**  Tim Berners-Lee invented HTML 1.0
-   **1993-**  HTML 1.0 was released. Not many developers were creating websites at this time.
-   **1995-** HTML 2.0 has been released. This includes all of the features of HTML 1.0, plus additional features. Until 1997, this was the standard markup language for designing and producing webpages.
-   **1997-**  HTML 3.0 was invented. Here, Dave Raggett introduced a fresh draft on HTML, which improved new features of HTML and gave more powerful characteristics for webmasters in designing websites. Unfortunately, the powerful features slowed down the browser in applying further improvements.
-   **1999-**  The widely-used HTML 4.0 was published. It was a huge success.
-   **2014-**  HTML 5.0 is released and used worldwide. It is said to be the extended version of HTML 4.01 which was published in 2012.

