---
title: Introduction To Tweening
template: docs.html
comments: true
hide:
  - navigation
---
# Tweening

This article will teach you about the concept of tweening, how tweening is useful in development and how to use the `TweenService` in Roblox.

## 1. What is "tweening"?

Inbetweening - **tweening** for short - is basically an animated process to create an illusion or effect, usually smooth, in transition between two keyframes in an animation or presentation.

![steps](https://i.imgur.com/s81yAPS.png)

Here's what the animation looks like in action:

![visual](https://i.imgur.com/3LJxRmd.png)

A comparison between tweening and no tweening, both have the same transition interval of 1 second:

![compare](https://i.imgur.com/7t4PdJs.png)

In this example, the **size** of both circles is being "tweened", both have the same transition interval of 1 second:

![compare_size](https://i.imgur.com/CGvn0v5.png)

As you can see, tweening did a good job in visualize the transition inbetween the 2 keyframes.

## 2. How useful is tweening?

I don't know about you, but I like my animation smooth and appealing. Besides that, tweening can also help you:

* Create animations / presentation easier, considering that tweening can reduce the amount of keyframes
* Execute multiple animation on a single instance (e.g. color, size, ...)
* Create VFX (Visual Effect)
* Simply make the animations less snappy and more easy-looking for the audience

Now that you have the basics and uses of tweening on hand, let's do some animation in Roblox!

---
## TweenService

### 1. What is TweenService?

`TweenService` is a built-in API Service, allowing developers to script the **tweening** effect on instances such as `BasePart` (Part, MeshPart, ...) and `GuiObject` (TextLabel, ImageLabel, ...) through interpolation in properties. Basically, this service creates animation on an object by changing it's properties in a particular way.

### 2. List of types that can be tweened

`TweenService` can only help animating properties of type in the following list:

* `number`
* `boolean`
* [`CFrame`](https://create.roblox.com/docs/reference/engine/datatypes/CFrame)
* [`Rect`](https://create.roblox.com/docs/reference/engine/datatypes/Rect)
* [`Color3`](https://create.roblox.com/docs/reference/engine/datatypes/Color3)
* [`UDim`](https://create.roblox.com/docs/reference/engine/datatypes/UDim)
* [`UDim2`](https://create.roblox.com/docs/reference/engine/datatypes/UDim2)
* [`Vector2`](https://create.roblox.com/docs/reference/engine/datatypes/Vector2)
* [`Vector2int16`](https://create.roblox.com/docs/reference/engine/datatypes/Vector2int16)
* [`Vector3`](https://create.roblox.com/docs/reference/engine/datatypes/Vector3)
* [`EnumItem`](https://create.roblox.com/docs/reference/engine/datatypes/EnumItem)

This list is important to remember, any other properties of type outside of this list can **NOT** be animated by `TweenService`.

??? note "What are some valid properties?"
    For instances like Part: `Position`, `CFrame`, `Size`, `Color`, `Transparency`, ...
    For UI elements: `Position`, `Size`, `Rotation`, `BackgroundColor3`, `TextColor3`, `BackgroundTransparency`, ...

---
## How do I use the TweenService?

### 1. Determine the target to tween
In this article, we are going to make a **dance floor** for our players. A little party area is fun for hanging out or show off your newly equipped emotes!

I made this little 3x3 dance floor so it's easier to demonstrate. Each gray tiles is a `Part` instance. You can design it however you want!

!!! attention "If you don't follow this example's structure, make sure:"
    - To make the code suit with your own structure
    - To have the list of valid properties in mind

![floor](https://i.imgur.com/kmzJqYc.png)

And here's how the Explorer hierachy looks like (**View -> Explorer** to open the Explorer window)
* The black bars go into the **"Bars"** folder, which will be ignored later on.
* The gray tiles go into the **"Tiles"** folder, which will be our **tweening targets**.
* The **"Control"** script, which we will write the **tweening code**.

![explorer](https://i.imgur.com/xRusspE.png)

### 2. Determine what to tween

Take a look at this simple but fancy dance floor we're going to make:

![dancefloor](https://i.imgur.com/MaEEF8R.gif)

As you can see, each floor tiles is smoothly changing it's color, creating a colorful atmosphere around our player. So, we will tween the tiles' `Color` properties  with the `TweenService`.

### 3. Determine how the tween will be, using `TweenInfo`

Now, take a closer look into the video. **There's a pattern on how the tiles are tweening**. To determine how they tween, we will use the `TweenInfo` datatype, as for **tween**ing **info**rmation.

`TweenInfo` have **only one** constructor, `TweenInfo.new()`, along with **six parameters**:

* `time: number` - Duration of the tween, in seconds
* `easingStyle: Enum.EasingStyle` - The "style", or how the tween looks like
* `easingDirection: Enum.EasingDirection` - The direction for the `EasingStyle` to occur
* `repeatCount: number` - The amount of times the tween will repeat itself
* `reverses: boolean` - Whether or not reverse to the original state after the initial tween
* `delayTime: number` - The duration that elapses before the tween play, in seconds

!!! attention "The order of the parameters are absolute"
    You can NOT rearrange this order. Hence, wrong parameter order can result in an unwanted tween behaviour or even an error.
    You must also give the correct type (they're written after the colon) for each parameter.

!!! tip "Repeat the tween indefintely"
    To make the tween repeat itself forever, set the `repeatCount` value to `-1`.

??? tip "Visual example of each EasingStyle and EasingDirection"
    Roblox has made a video covering all 6 `EasingStyle` and 2 `EasingDirection`:
    ![ease](https://developer.roblox.com/assets/blt164bc3fd53630e3a/Easingstyle.gif)

??? tip "The default values of TweenInfo.new()"
    Assume you're lazy and you don't want to type out all 6 parameters, `TweenInfo.new()` will automatically fill the missing arguments with the follow values:
    `time`: 1
    `easingStyle`: `Enum.EasingStyle.Quad`
    `easingDirection`: `Enum.EasingDirection.Out`
    `repeatCount`: 0
    `reverses`: false
    `delayTime`: 0


I will cover them all in this example, so pay attention!
Open the control script, type in the following code. The comments will help you understand what line contribute what to the tween animation:

```lua
local tween_info = TweenInfo.new( -- Remember: parenthesis () not brackets {}
    1, -- The color will change in 1 second
    Enum.EasingStyle.Linear, -- Tween at a constant speed
    Enum.EasingDirection.In, -- In or Out doesn't matter, as the tween is in constant speed
    -1, -- Automatically repeat the tween indefinitely, so we don't have to
    true, -- Reverse to the original color, for a little colorful effect
    0 -- Make the tween play instantly
)
```

!!! tip "You can adjust the values to your liking"
    Make sure to give the correct type for each parameter.

### 4. Create a tween using `TweenService:Create()`

To create a tween sequence, we will use the `TweenService:Create()` method. This method will return a `Tween` sequence for us to interact in the next section.

`TweenService:Create()` has **3 parameters**, the order is absolute:

* `instance` - The target instance to tween
* `tweenInfo` - The `TweenInfo` for the tween sequence
* `propertyTable` - The target properties to tween

!!! attention "The `propertyTable` parameter"
    `propertyTable` takes a `dictionary` table as an argument. The syntax is as the following:
    ```lua
    local target = {
        <property_name_1> = <target_value_1>,
        <property_name_2> = <target_value_2>,
        ...,
        <property_name_n> = <target_value_n>
    }
    ```
    
Remember those **gray tiles** in the **"Tiles"** folder? That's our targets to tween. **But,** the `instance` parameter only takes **1** instance. So, we will have to create **9** tween sequences for our dance floor.

We can use a `for` loop to simutaneously create one tween sequence for each tiles in the folder.

??? attention "Regarding the following code"
    While this code is not the most efficient way to tween multiple instances, it is written for the sake of beginners. You can, later on, alter the code and the overall structure to your liking.

```lua
-- Get the service with the GetService() method
local TweenService = game:GetService("TweenService")

-- Get the "Tiles" folder, which is holding our gray tiles
local tiles = script.Parent.Tiles

-- The TweenInfo we created earlier, I have collapsed into one line
local tween_info = TweenInfo.new(1, Enum.EasingStyle.Linear, Enum.EasingDirection.In, -1, true, 0)

-- We will determine the target color for the tiles with a dictionary
-- "Color" is one of the tile's properties. To see all the properties of a part, go to "View" -> "Properties" to toggle the "Properties" window 
local target_color = {
    Color = Color3.fromRGB(100, 57, 64) -- This is red, you can change to whatever color you want
}

-- The following code require basic understandings of the for loop
-- tiles:GetChildren() return an array containing all the tiles
for i, tile in ipairs(tiles:GetChildren()) do
    -- Create a tween sequence
    local tween = TweenService:Create(
        tile,           -- The gray tile instance
        tween_info,     -- The tween info
        target_color    -- The target color
    )
end
```

Now, we have successfully assign 9 tween sequences to 9 tiles. **But we're not done yet**. When you play test the game, you will see the dance floor is just sitting still and nothing happen. This is because we have just created the tween sequences, **but we haven't actually play them yet.** The following section will help you with that.

### 5. Play the tween using `tween:Play()`
This method is self-explanatory. It will play the tween sequence the moment it is called.

!!! attention "Note"
    Keep in mind that this method is **exclusive** to the **tween sequence** (created by the `TweenService:Create()` method). This is **NOT** a method of the  `TweenService`.

We just need to add a single line of code to call this method and play the tween:
```lua
local TweenService = game:GetService("TweenService")
local tiles = script.Parent.Tiles

local tween_info = TweenInfo.new(1, Enum.EasingStyle.Linear, Enum.EasingDirection.In, -1, true, 0)

local target_color = {
    Color = Color3.fromRGB(100, 57, 64)
}

for i, tile in ipairs(tiles:GetChildren()) do
    local tween = TweenService:Create(tile, tween_info, target_color)
    tween:Play() -- Play the tween
end
```

Now we play test again:

![floor](https://i.imgur.com/pjhKepX.png)

It's actually a bad timing GIF, so hopefully it will look better on your side! But more importantly, **you have successfully know how to use the `TweenService` to make a simple tween animation!**

??? question "Exercise: Complete the dance floor at the beginning (open for solution)"
    As you can see from the original video, there are 2 different tweening patterns. So let's do that: The tiles that create the cross shape will be named "Tile1", the other four, "Tile2".
    Initially, all 9 tiles are gray colored, so how does the video shows blue and red? The trick here is:
    - Instead of gray, the tiles are colored with their designated colors at the beginning: Tile1 is blue, Tile2 is red.
    - Set the color target: Tile1 will be tweened red, while Tile2 will be tweened blue.
    - Distinguish the tiles using **conditional statements**.
    Since we set the tween `reverses` property to `true`, it will reverse back to it's original color. Instead of gray, it will be red and blue.
    Here's how the code looks like:
    ```lua
        local TweenService = game:GetService("TweenService")
        local tiles = script.Parent.Tiles
        
        local tween_info = TweenInfo.new(1, Enum.EasingStyle.Linear, Enum.EasingDirection.In, -1, true, 0)
        
        local color1 = {
            Color = Color3.fromRGB(255, 89, 89) -- Red, for Tile2
        }
        
        local color2 = {
            Color = Color3.fromRGB(4, 175, 236) -- Blue, for Tile1
        }
        
        for i, tile in ipairs(tiles:GetChildren()) do
            local tween -- A placeholder for the tween
            
            -- Filter the tiles
            if tile.Name == "Tile1" then
                tween = TweenService:Create(tile, tween_info, color1)
            else
                tween = TweenService:Create(tile, tween_info, color2)
            end
            
            tween:Play() -- Play the tween
        end
    ```

### 6. `tween:Cancel()`, `tween:Pause()` and `tween:Resume()`
These methods is self-explanatory in name. This section will help you **distinguish the differences** between `tween:Cancel()` and `tween:Pause()`.

Both methods will **halt** the playing tween at the current interpolation at the moment they're called. This means that the target instance will **not** be reset to it's original state before tweening is initiated.

A quick visual example, both circles have the tween duration of 1 second. `tween:Cancel()` is called after 0.5 second. The same effect is applied when `tween:Pause()` is used.

![cancel](https://i.imgur.com/xzmrZUI.png)

**Here are the differences between the 2 methods:**
* `tween:Pause()` can be resumed by either `tween:Play()` or `tween:Resume()`. Upon resuming, **the tween will continue at the moment it was halted**.
* `tween:Cancel` can be continued by the `tween:Play()` method **only**. Upon continuing, **all current tweening information will be reset**. For example: it will take full duration of the tween to finish the animation.

### 7. The `tween.Completed` event

`tween.Completed` is an Event ([`RbxScriptSignal`](https://create.roblox.com/docs/reference/engine/datatypes/RBXScriptSignal)) that fires after the tweening process is completed or cancelled by  the `Cancel` method.

`tween.Completed` pass 1 parameter, the `playbackState`. You can see all types of `playbackState` in [this page](https://create.roblox.com/docs/reference/engine/enums/PlaybackState).

```lua
tween.Completed:Connect(function(playbackState)
    print(playbackState)
end)
```

!!! info "playbackState" is likely to be one of 2 values:
    - `Enum.PlaybackState.Completed`: If the tween completed successfully.
    - `Enum.PlaybackState.Cancelled`: If the tween is cancelled by the `Cancel` method before completion.

---
## Additional sources
* [Official Roblox TweenService documentation](https://create.roblox.com/docs/reference/engine/classes/TweenService)
* [Official Roblox Tween sequence documentation](https://www.w3schools.com/tags/ref_httpmethods.asp)
* [Detailed Roblox documentation regarding Easing Styles and Directions](https://create.roblox.com/docs/reference/engine/enums/EasingStyle)
* [Roblox guide on User Interface Tweening](https://create.roblox.com/docs/building-and-visuals/ui/tweening-user-interface-animations)
* [More about the concept of Tweening (wikipedia)](https://en.wikipedia.org/wiki/Inbetweening)

---
## That's about it
Use TweenService to further improve in-game experience as you please. Good luck!

---