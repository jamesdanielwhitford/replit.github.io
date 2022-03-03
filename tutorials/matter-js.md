# Matter.js with Replit

Matter.js is 2D physics, javascript engine that is awesome when it comes to creating 2D animations. Using Replit, we can create matter.js animation projects on the platform.

In this tutorial, we're going to learn about how we can use matter.js with replit by creating a 2d animation of our own.

## What we'll discuss

Here's what this tutorial covers:

* Matter.js on Replit
* How to create a 2D animation
* Uses of Matter.js

You can find the code for this tutorial at https://replit.com/@ritza/matter-js or check out the embedded repl below.

## Matter.js on Replit

Using the Replit platform, we can create an HTML repl to create access the matter-js library. We can import the matter-js into our repl and access all the awesome functions it has to create a 2D animation.

There's a lot of information on [getting started with matter.js](https://github.com/liabru/matter-js/wiki/Getting-started) if you're unfamiliar with the engine. If you would like to explore more functions that you can use to improve your projects or find demo projects, you can check out the [matter.js](https://brm.io/matter-js/) website.


## Getting started with the setup

We'll get started by navigating to our Replit dashboard and clicking on the "Create" button for a new repl. We'll Choose "HTML" as our template language and once we've we've chosen a name we can go ahead and create our repl.

![create repl](create-repl.png)

On the Replit workspace, notice the "script.js" file, this is where we'll add the code logic for all animation and we'll configure the "index.html" file to show live updates of our changes.


## How to create a 2D animation

We're going to create an animation that generates a bunch of rods from a height that will collect at the bottom of the screen. Let's get started by importing the matter-js package into our application.

 We want to add this package and the "script.js" file to the "index.html". So we'll include them in the head and body tag of our "index.html" file, respectively. 

Your index.html file should look like this:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Matter js</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/matter-js/0.18.0/matter.js"></script>
</head>
<body>
    <script type="text/javascript" src="script.js"></script>
</body>
</html>
```

That's it, we're done with the HTML file for the rest of the tutorial. We'll now focus only on the "script.js" file to create our 2D animation.

We'll start with creating variables for the module's main class functions. Just to avoid writing out the long functions when we want to use them.

```javascript
var Engine = Matter.Engine,
    Render = Matter.Render,
    Runner = Matter.Runner,
    Bodies = Matter.Bodies,
    Composite = Matter.Composite;


```

We'll want to create an engine and render variable that we will use to add the animations to our display window for us.

```javascript
var engine = Engine.create();

var render = Render.create({
    element: document.body,
    engine: engine,
  options:{
    wireframes: false} 
});

render.canvas.width = window.innerWidth
render.canvas.height= window.innerHeight
```

"document" refers to the "index.html" file, where we'll render our animations, and setting "wireframes" to false will allow us to color our rods. We also use `render.canvas` to set the width and height of our animation screen or "world" to fit the display screen.

For our rods, we'll create a function that generates rods for us and use an interval to keep generating them after a set time. The "ground" variable represents a platform the rods can land on and we added it to our animation world by passing it to `Composite.add()` in an array. Composite is used to add a group of objects to the world. That is why we pass objects to it in an array.

```javascript
var ground = Bodies.rectangle(window.innerWidth/2, window.innerHeight,800,20,{isStatic:true})

function addRods(){
    let rod = Bodies.rectangle(window.innerWidth/2,200,20,80,{
      render: {
         strokeStyle: 'black',
         lineWidth: 3
    }
    });
    Composite.add(engine.world, [rod])
}

setInterval(addRods,200)
Composite.add(engine.world,[ground])
```

Now we can run render, as well as the engine to see our animation.

```
Render.run(render);
var runner = Runner.create();
Runner.run(runner, engine);

```

Click on run to see the animation.

![random rods](random-rods.png)

That is it for our 2D animation.

## Uses of Matter.js

There are lots of awesome demo projects from [matter.js](https://brm.io/matter-js) that you can try out or find inspiration from. Matter-js is an engine that provides a good entry point for animators and illustrators to learn code and still embrace their creativity. It's also great for creating nice interactive designs for a website or just any side project.

It's fun to learn and it has so much more tools you can use to come up with unique projects.

### Things you can try

Here are some cool projects you can try out to challenge yourself:
 
* Create Newtons cradle
* Create a wrecking ball to knock over a stack of objects.


<iframe frameborder="0" width="100%" height="500px" src="https://replit.com/@ritza/matter-js?embed=true"></iframe>
