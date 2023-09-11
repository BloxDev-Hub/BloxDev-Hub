---
title: Introduction To Size and Position 
template: docs.html
comments: true
hide:
  - navigation
---

# Changing Size and Position 
Previously we explained vectors, their types, addition, and product of vectors. Now we will move further and talk about its usage in changing positions and sizes. Once you have cleared your mind regarding vectors, you are surely able to understand their usage in Roblox.

## Changing Size
When you are changing the size of a base part, the origin of the vector is at the centre of the base part.
We have a part in the workspace of size (6,6,6).

![FirstPivot](https://imgur.com/027ZDGE.png)

The blue point in the middle of the part represents the pivot point however it is in the centre, we will use this point as the origin. Now it's time to change the size of this part.

We will increase its size on the y-axis by 8 studs. (As whole, it will be 14 studs on the y-axis)

```lua
workspace.Part.Size = Vector3.new(6,14,6)
```

![Biggerpart](https://imgur.com/T3Y4qkH.png)

You can see, that our part is much bigger now. If you look carefully, you will notice the size is increased on both sides of y-axis (positive y-axis and negative y-axis). In Roblox engine, if you increase the size of a part by using a script, the engine tends to keep it in the same position. When changing size on the positive y-axis, the position of the part would have changed as the center of the part will be moved above. Because we increased the size by 8 studs, it will increase 4 studs on the positive y-axis and 4 studs on the negative y-axis. Similarly, size can be increased on other axes.

## Changing Positions
While changing the position of a base part. The origin of a vector is the center of the world. We have a part in the center of the world which means, its position is `(0,0,0)`.

![Centerpos](https://imgur.com/lhb8Hdg.png)

We will change its position to `(8,6,8)`.  We will use a vector having magnitude of 8 studs on the x-axis, 6 studs on the y-axis, and 8 studs on the z-axis. This can be done by 

```lua
workspace.Part.Position = Vector3.new(8,6,8)
```

Here we go

![newpos](https://imgur.com/D9jXDBP.png)

It is indeed very easy if your concepts of vectors are clear. You might have a question, about why I explained vectors in that much detail when it was just this and that. At the basic level, you would not need to compute vectors that much but I assure you that you will need them if you want to do stuff like projectile motion, linear velocities, etc. Let's get back to our topic.

### Moving a part relative to its position
Previously we were changing position from the center of the world. Now if you want to move a part 4 studs above which is initially placed at `(8,6,8)` from origin.

![newpos](https://imgur.com/D9jXDBP.png)

We will simply add a vector `(0,4,0)` in the position vector of the part. This will be done through [additon of vectors](https://rodevs-helpers.github.io/Helpers-Documents/Luau-Learning/Vector3_Part_2/#addition-of-vectors).

```lua
--Getting initial position (8,6,8)
local initial_position = workspace.Part.Position
--adding vectors
local new_position = initial_position + Vector3.new(0,4,0)

workspace.Part.Position = new_position
```

![Abovepos](https://imgur.com/i3YsYWe.png)

Congrats! we succeeded in moving it 4 studs above (positive y-axis).
Similarly, you can move it on the x and z axes.

```lua
--Geeting initial position (8,6,8)
local initial_position = workspace.Part.Position
--adding vectors
local new_position = initial_position + Vector3.new(9,4,3)

workspace.Part.Position = new_position
```

![otherpos](https://imgur.com/dphtWwM.png)

## Closing!
That's pretty much of it. Hope you enjoyed reading it. In case of any mistake, typos, etc. Please report the article. You can also give us reviews [here](https://rodevs-helpers.github.io/Helpers-Documents/Others/Help_Us%21/)