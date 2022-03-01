# Exploring Kaboom Draw with Replit

If you're familiar with Replit's game development framework [kaboomjs](http://kaboom.com), Here's an awesome tutorial on how to create images or animations using code, with Kaboom on the Replit platform.

In this tutorial, we're going to learn about how to use kaboom draw by creating a little animation.

## What we'll discuss:

* Kaboom Draw on Replit
* How to create an animation
* Uses of Kaboom draw

You can find the code we'll use in this tutorial at https://replit.com/@ritza/kaboom-draw or try out the embedded repl below.


## Kaboom draw on Replit

Kaboom draw is actually a great extension of kaboom we can use for creating and sharing awesome animations or illustrations. By creating a "Kaboom Draw" repl, we can use most of kaboom's drawing functions to make our creative projects.

The repl provides a few template projects in an "examples" folder with awesome animations that we can learn from and get inspired for our own ideas. From those existing templates, we can learn more of the varying functionalities of drawing functions from kaboom to really enhance our skills.

Also, we can use [kaboom's](http://kaboomjs.com) website to learn about other functions we want to use. 

## Create a repl

We'll get started by navigating to our Replit dashboard and clicking on the "Create" button. Choose "Kaboom Draw" as our template language and once we've we've chosen a name we'll create our repl.

![creating a repl](create-repl.png)

On the Replit workspace, notice the "draw.js" file, this is where we add our code logic for all our animations.


## How to create an animation

Let's open up the "draw.js" in our workspace and clear all of the existing code in the file. Notice the small toolbar at the bottom of the editing pane with drawing tools.

We'll be using some of these shapes for our animation. To add the shape, we can drag and drop it on the pane, and when we do that, kaboom provides some template code we can use to modify the object behaviour and appearance.

We're going to create an animation similar to this one:

![animation](seeds.gif)

In our "draw.js" file, let's add some code to create our background for the animation.

```javascript
drawRect({
	pos: vec2(0),
	width: width(),
	height: height(),
	color: rgb(0, 0, 0),
})

for (let i = 0; i < 3; i++) {
	drawCircle({
		pos: vec2(rand(0, width()), rand(0, height())),
		radius: 1,
		color: rgb(255, 255, 255),
	})
}
```
  This provides a dark space-like background for our code.

  Next, we're going to use a for loop to generate our pentagon shapes, to avoid repetitive code. Add the following code to your file:

```javascript
for (let i = 0; i < 15; i++) {

	drawPolygon({
			pos: vec2(240, 140),
	pts: [
		vec2(0, -48),
		vec2(-64, 0),
		vec2(-32, 64),
		vec2(32, 64),
		vec2(64, 0),
	],
    scale:.4 + i/5,
    origin: "center",
    rotation: 0,
    angle:12*time(),
	  opacity: -10,
		outline: {
		width: 1,
		color: Color.fromHSL(
			(i * 0.1 + time() / 2) % 1,
			0.6,
			0.8
		),
	},		
	})
}
```

Then for the circle, let's add this last bit of code:

```javascript
drawCircle({
  pos: vec2(240, 170),
  radius: 48,
  opacity: -10,
  scale: 4.4,
  outline: {
  width: 0.6,
  color: Color.fromHSL(
  			(0.1 + time() / 2) % 1, 0.6,0.8
  		),
},})
```

Once we run this, we'll see a nice little animation of rainbow colors that looks like this:

![animation](animation.png)

That's our animation!

### Components

Each time we use shapes, we are creating an instance of that shape, whose qualities we can modify. So, when we drag these objects onto the editing pane some of those qualities are specified for us, which help us better understand the uses of some functions.

Here are some more functions we can learn:

`pos()` - Used to set the position of the objects.
`width()`, `height()` - Specify the dimensions of the object.
`opacity()` - Used to make objects tranparent in the center.
`fromHSL` - Used to create a rainbow color-effect for the shape objects.
`scale()`- Used to scale up the objects.
`outline()` - Used to specify appearance of the shapes outline.


## Uses of Kaboom draw

Kaboom Draw can be used by anyone, designers or developers, even illustrators to make great animations, for either a website, a presentation or simply to play around with.

It is a handy tool and it makes it fun to get started on coming up with creative projects.


### Things to try

Here are some things you can try out to challenge yourself with Kaboom Draw:
  
* Create a disco ball
* illustrate music lyrics with the text tools

<iframe frameborder="0" width="100%" height="500px" src="https://replit.com/@ritza/kaboom-draw?embed=true"></iframe>
