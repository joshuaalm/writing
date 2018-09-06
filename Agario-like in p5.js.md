# Agario-like in p5.js

[TOC]

## What you should know

Before you begin, you should know how to use basic p5.js functions, including:

- point()
- ellipse()
- text()
- line()

and be familiar with the math concepts involved which are

- 2D coordinate systems (x and y)
- Pythagorean theorem

## Basic shapes

The shapes in our game are very simple:

1. The player is a big round blob
2. The food is a tiny round blob

For the player, we can use an `ellipse()` and for the food we can use a `point()`, though we may want to use a `strokeWidth()` that makes the food easier to see.

## Game mechanics

The player's blob will follow the mouse, and get bigger when it eats bits of food.  

## Make the player's shape

## Make the player follow the mouse

We can make the player's character shape move directly with the mouse, simply by writing

```javascript
ellipse(mouseX,mouseY,size,size);
```

but that wouldn't be much of a challenge.  It would make for a better game if the player always moved *toward* the mouse cursor, but at a speed that is inversely proportional to it size.

## Generate random bits of food

## Collision detection

The player and the food bits are both shaped like circles, which keeps the drawing simple, and is somewhat convenient.  But how do we tell our game when to increase the player's mass?  It's not enough to say that the position of a piece of food and the coordinates of the player's position are the same, since this means the collision will only be detected when the player is centered over the food.  It's more realistic if the collision is detected at the edge of the player's shape.

The shortest distance between the player and the food would therefore be the sum of their radii.  In the case of the player, the radius is 

## Make the food disappear (and reappear)

## Make the player's mass increase with each piece of food eaten

Now that our game detects when a player 'eats' food through our collision detection algorithm, we can create a variable to hold the number of units of mass our player has, and continues to attain, and from that we can increase our player's size.



Since our player is a single cell, we assume he's flat, like on a microscope slide (even though we know cells aren't really flat, it's simpler for viewing real cells and game cells as if they have at least uniform thickness) and therefore the mass is proportional to its volume -- assume a thickness of 1 unit and uniform radius.  Therefore, the mass is now equal to the area of the circle shape.  You should be familiar with the formula for area of a circle, but we'll state it here before converting it to a code-friendly format, and then using the resulting computation in our drawing code.

`A = pi * r^2 `

$A = \pi\times r^2$

What part of this equation do we need to draw the circle?  The radius, of course.  That's the part we'll place into the `ellipse(x,y,width,height)` function, in place of the width and the height, in order to make a circle.

So let the mass be A, and the size be the radius:

`mass = pi * size^2`

Now solve for the size:

`mass / pi = pi * size^2/pi`

`sqrt(mass/pi) = sqrt(size^2)`

`sqrt(mass/pi) = size`

In JavaScript, we can save the calculation in the `size` variable like so:

`size = sqrt(mass/pi)`

And then we can use the size variable when drawing our cell:

`ellipse(cellX,cellY,size,size)`