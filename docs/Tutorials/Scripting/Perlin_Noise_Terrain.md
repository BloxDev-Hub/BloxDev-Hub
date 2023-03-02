---
title: Perlin Noise Terrain
og_image: https://i.imgur.com/z0deBFG.png
---

# Introduction
In this tutorial, we will be generating some (blocky) terrain using **[Perlin Noise](#what-is-perlin-noise)**, which can allow us to infinitely generate terrain, by using the numbers it generates as a height value for each of our chunks.

### What is Perlin Noise?
**Perlin Noise** ([Wikipedia](https://en.wikipedia.org/wiki/Perlin_noise)) is a type of gradient noise (commonly implemented as a two or three-dimensional function) developed by Ken Perlin.  

In Roblox, it is implemented with the [math.noise](https://create.roblox.com/docs/reference/engine/libraries/math#noise) function, which takes 3 (2 optional) arguments. The function takes in numbers and returns a fixed Perlin noise value for that coordinate.  

Some things to know: 
- The optional arguments that you did not pass in will be interpreted as 0.
- If x, y, and z are all integers, the return value will be 0.
- For values between 0 and 1, the return value will gradually fluctuate between -0.5 and 0.5.
  
#### Why not just random?

The whole reason we are using Perlin Noise and not just using random numbers is that we want our terrain to be smooth and 'realistic'. Take a look at this illustration for example:  

<img src='https://assets.runemadsen.com/random_vs_noise-8670d2707d1d767afad267d2b8182538_medium.jpg' style='display:block; margin:auto; margin-bottom:20px'>
  
The top graph is randomly generated, but the bottom uses Perlin noise for a smoother yet still random distribution.

## Scripting

### Setup
Okay, with all that out of the way we can start creating our random terrain generation.  

Let's start with making our chunks.  

<img src='https://imgur.com/c0UXYEv.jpg' style='display:block; margin:auto; margin-bottom:20px'>

I've deleted the baseplate and added a part with the size 10,10,10. Our Y size does not matter at this point, but we will talk about that later. We can move this chunk to ServerStorage, where we will retrieve it later and use it to build our terrain with a script.

Let's add a script into ServerScriptService, and start writing our code. First of all, of course, reference our chunk. Then, let's get some useful constants in place.

```lua
local chunk = game.ServerStorage.chunk
local gap = chunk.Size.x
local intensity = 1/200
```

The idea here with "gap" (I will explain intensity a bit later) is that I will use it in our calculations when creating a grid of chunks, it is just the space that will be in between one chunk and another. Defining it in this way also allows us to change the size of our chunks at any time while keeping the terrain seamless (at least when the x and y sizes are the same).

### Grid

Let's make a nested for loop here to generate a grid of these chunks.

```lua
for xOffset = -50, 50 do
    for yOffset = -50, 50 do
        local height = 0
        local clone = chunk:Clone()
        clone.Position = Vector3.new(xOffset * gap, height, yOffset * gap)
        clone.Parent = workspace
    end
end
```
And here we go!

<img src='https://imgur.com/Atm1utY.jpg' style='display:block; margin:auto; margin-bottom:20px'>

This is a bit more code than just defining our constants earlier, so let me break it down.  
1. Our nested for loop, getting us x and y values from -50 to 50 lets us get positions for our chunks by multiplying that with the gap.
2. We set a height variable, which is a surprise tool we will use later. 
3. We clone our chunk from ServerStorage and set its x and y to the values from our current iteration of the nested loop, multiplied by the gap.
4. We set the cloned chunk's parent to workspace, and repeat until all 1000 of our chunks are done.

Personally, to make this a bit cleaner and more clear I would refactor this code to be put into a function that just takes the side length of the grid we want to create and a center point, so we can go ahead and do this.

```lua
function createGrid(sideLength: number, centerPoint: Vector3)
    local half = sideLength/2
    for xOffset = -half, half do
        for yOffset = -half, half do
            local coordinates = {
                x = centerPoint.X + xOffset * gap;
                y = centerPoint.Z + yOffset * gap
            }
            local height = 0
            local clone = chunk:Clone()
            clone.Position = Vector3.new(coordinates.x, centerPoint.Y + height, coordinates.y)
            clone.Parent = workspace
        end
    end
end
```
!!! info Type Checking Function Arguments
    Don't mind the weird stuff next to the function arguments if you don't understand them, it's just making sure the arguments we pass in are the correct type using Luau [type checking](https://luau-lang.org/typecheck).

You may notice I added the coordinates table, this is because we will need those x and z coordinates for not only the clone's position but to use with the noise function later. The math is also changed a bit, we need to add the components of our centerPoint to x and y (and height) so that our centerPoint argument is working as intended, offsetting our grid to be centered on that point. The rest of this code is the same as earlier, just refactored to work as a function with arguments for sideLength.


And calling this function to do the same thing we did earlier is as simple as this: 
```lua
createGrid(100, Vector3.new(0,0,0))
```

There we go! We have a simple way to create a grid of chunks around a certain point in our workspace, and we can change the height associated with each chunk by simply changing what we assign our height variable to inside the function.  

### Using Perlin Noise

You see, the way we will be making our terrain look like an actual landscape will be by changing the height of each of our chunks to a number based on the Perlin noise value at that coordinate *multiplied by our intensity*. (will talk more about this soon)  

Now, Let's change our height variable to use the thing we've been talking about for the past 3000 paragraphs!

We'll start by calling `math.noise`, passing in our x and y values multiplied by intensity.

```lua
local height = math.noise(x * intensity, y * intensity)
```

So, what exactly *is* our intensity variable? Well, when getting values from Perlin Noise, the closer together the coordinates you passed in are the closer their value will be. (the whole point of Perlin noise, as we looked at [earlier](#why-not-just-random))

The smaller our intensity value is, the smoother the terrain will be, and vice versa of course.  

Now, with this small change in place, you can run your game and... 

<img src='https://imgur.com/5hyvlGg.jpg' style='display:block; margin:auto; margin-bottom:20px'>

Hmm. It still just looks like a flat grid. Let's take a closer look at one of our chunk's size properties.

<img src='https://imgur.com/z7RPLzp.jpg' style='display:block; margin:auto; margin-bottom:20px'>

Taking a closer look, the chunks all have different y values, but as you can see they are very small. That's an easy fix, let's multiply our height by 100 in our variable 
```lua
local height = math.noise(x * intensity, y * intensity) * 100
```
And run our game again...

<img src='https://imgur.com/OZfolY4.jpg' style='display:block; margin:auto; margin-bottom:20px'>

There we have it, some blocky terrain we have generated in only 20 lines of code!  

### Seeded Generation

Now, you will notice that when generating this terrain, it is the same every time you run the game. As you may remember, another property of Perlin noise is that given the same coordinates, you will receive the same value every time. To change this, we can use the third argument as our seed in the math.noise function.

Adding 1234 for example gets us this:

<img src='https://imgur.com/XVNVRt4.jpg' style='display:block; margin:auto; margin-bottom:20px'>

Let's add a seed argument to our createGrid function...

```lua
function createGrid(sideLength: number, centerPoint: Vector3, seed: number?)
```

...and call the function passing math.random() as the seed.

```lua
createGrid(100, Vector3.new(0,0,0), math.random())
```

And our random terrain generator is done. Feel free to play around and generate whatever size grids you want, or even try and make your own procedurally generating map using our centerPoint argument to generate grids wherever people are about to walk. 

### Cleaning Up

For now, though, I want to turn this monstrosity 

<img src='https://imgur.com/Al1MGfO.jpg' style='display:block; margin:auto; margin-bottom:20px'>

Into something nicer and easier to use for whatever you may need, like this

<img src='https://imgur.com/0ZkyXJZ.jpg' style='display:block; margin:auto; margin-bottom:20px'>

It may not look very helpful as it is in the explorer, but simply naming them by their coordinates will help a lot if you ever want to refer to a specific chunk via a script when all you have is a position.

This change is simple, in our createGrid function simply add a line where you change the clone's name to the elements of our coordinates table separated by a colon. Also, create a folder named TerrainGrid (or whatever else you want, be careful not to name it something that is already in use though, such as Terrain) inside workspace, and instead of setting the clone's parent to workspace directly insert it into that folder.

```lua
clone.Position = Vector3.new(coordinates.x, centerPoint.Y + height, coordinates.y)
clone.Name =  coordinates.x .. ":" .. coordinates.y
clone.Parent = workspace.TerrainGrid
```

### Extra


#### Colors

Before we finish, let's make our grid a bit more colorful than just a flat grey.

To do this, we can use our height variable to manipulate the color of each block to give it the look of a colorful topographic map.

Add yet another line to our createGrid function, next to all of our other lines which change the properties of our clone. 

```lua
clone.Position = Vector3.new(coordinates.x, centerPoint.Y + height, coordinates.y)
clone.Color = color
clone.Name =  coordinates.x .. ":" .. coordinates.y
clone.Parent = workspace.TerrainGrid
```

Now, of course, the color variable here doesn't exist. We need to figure out how we can use our height variable to scale across a color spectrum.  
I think the logical first step here would be to figure out the bounds of height, what are the minimum and maximum values it goes to?

After extensive research (skimming through the Perlin Noise [wikipedia page](https://en.wikipedia.org/wiki/Perlin_noise) again), I found "Noise functions for use in computer graphics typically produce values in the range [-1.0,1.0] and can be scaled accordingly." Our height variable is just a Perlin noise value multiplied by 100, so logically our bounds are -100, 100.

To change this to a 0-1 scale, let's
1. Add 100 to get a 0-200 scale
2. Divide by 200

Now we use this new 0-1 scaled number in an HSV value as the hue, 
```lua
color = Color3.fromHSV((height+100) / 200, 1, 1)
```
And now we have some colorful blocks.
Play around with this coloring, I noticed that the height never often reached past 90 so I replaced 100 with 90 and 200 with 180. I also wanted the lower values to be cooler, so I simply inverted the value by subtracting it from 1. 

Using this 
```lua
local color = Color3.fromHSV(1 - (height+90) / 180, 1, 1)
```
Gave me this:

<img src='https://imgur.com/RVrLCjK.png' style='display:block; margin:auto; margin-bottom:20px'>

#### Big Chunks

Let's change up the dimensions of our basic chunk, and see what happens. 

Changing it to a 100x100x100 cube gives me this... 

<img src='https://imgur.com/Jp7Igkk.jpg' style='display:block; margin:auto; margin-bottom:20px'>

...which is not very nice looking. What went wrong here?

Well, our intensity and height are not scaled to our block size. The intensity being unscaled means the coordinates used for our noise value will be very far apart. Our height being incorrectly scaled will make our terrain look far too flat when our intensity is fixed. 

Scaling both of these values (and our color variables) to "gap" will fix our problems. My code looks like this: 
```lua
function createGrid(sideLength: number, centerPoint: Vector3, seed: number?)
    local half = sideLength/2
    for xOffset = -half, half do
        for yOffset = -half, half do
            local coordinates = {
                x = centerPoint.X + xOffset * gap;
                y = centerPoint.Z + yOffset * gap
            }
            local height = math.noise(coordinates.x * intensity, coordinates.y * intensity, seed) * (gap*10)
            local color = Color3.fromHSV(1 - (height+9*gap) / (18*gap), 1, 1)
            local clone = chunk:Clone()
            clone.Position = Vector3.new(coordinates.x, centerPoint.Y + height, coordinates.y)
            clone.Name =  coordinates.x .. ":" .. coordinates.y
            clone.Color = color
            clone.Parent = workspace.TerrainGrid
        end
    end
end
```

And the final outcome of this tutorial is this:

<img src='https://imgur.com/z0deBFG.jpg' style='display:block; margin:auto; margin-bottom:20px'>

It may look the exact same as the 10x10x10 but of course, this picture was taken by a flying omnipotent entity, if you were to walk around in the actual map it would be huge.

## End

I hope this tutorial brought you everything you need to know regarding Perlin noise and how to use it to generate some infinite and random terrain in Roblox Studio.
