# Exploring Kaboom Draw with Replit

If you're familiar with Replit's game development framework [Kaboom.js](http://kaboomjs.com), you'll be interested to know that you can create images or animations on the Replit platform using code with a Kaboom extension called Kaboom Draw.

In this tutorial, we'll introduce you to the basics of Kaboom Draw by creating a little animation similar to this one:

![animation](seeds.gif)

## What we'll cover:

* Kaboom Draw on Replit
* How to create an animation
* Uses of Kaboom Draw

You can find the code we use in this tutorial at https://replit.com/@ritza/kaboom-draw or try out the embedded repl below.

## Create a repl

Let's get started by navigating to our Replit dashboard and clicking on the "Create" button. Choose "Kaboom Draw" as your template language, and give your repl a name.

![creating a repl](create-repl.png)

Notice that the repl includes an "examples" folder – you might like to explore the example animations in there, see what functions are possible and get a little inspired. You can use [Kaboom's website](https://kaboomjs.com) to learn about other functions you may want to use to create your own animations.

In our Replit workspace, find the "draw.js" file. This is where we'll add our code logic.

## How to create an animation

Open "draw.js" in your workspace and clear all of the existing code in the file.

Notice the small toolbar at the bottom of the editing pane with drawing tools. We'll be using some of these shapes for our animation. To add a shape, we can drag and drop it into the code editor. Kaboom provides some template code that we can use to modify the object's behaviour and appearance.

Let's add some code to create a background for our animation. In the "draw.js" file, add this code:

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
  
  Here we're adding a dark, space-like background.

  Next, we're going to use a for loop to generate our pentagon shapes. This allows us to avoid repetitive code. Add the following to your file:

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

Run your repl now, and you should see a nice little animation of rainbow colors that looks like this:

![animation](animation.png)

### Components

Each time we use a shape, we create an instance of that shape with qualities we can modify. When we drag and drop these objects into the editing pane, some of these qualities are specified for us, which helps us better understand the uses of some functions.

Here are some more functions we can learn:

* `pos()` - to set the position of the objects
* `width()` and `height()` - to specify the dimensions of the object
* `opacity()` - to give objects a tranparent center
* `fromHSL` - to create a rainbow color-effect for the shape objects
* `scale()`- to scale the objects
* `outline()` - to specify the appearance of the shape's outline

## Uses of Kaboom Draw

Kaboom Draw can be used by anyone, designers or developers, even illustrators to make great animations. These animations could be used for a website or a presentation, but they're also fun to simply play around with!

### Things to try

Here are some things you can try out to challenge yourself with Kaboom Draw:
  
* Create a disco ball
* Illustrate song lyrics with the text tools

<iframe frameborder="0" width="100%" height="500px" src="https://replit.com/@ritza/kaboom-draw?embed=true"></iframe>
