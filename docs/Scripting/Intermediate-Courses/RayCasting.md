---
title: Introduction To Raycasting!
template: docs.html
comments: true
hide:
  - navigation
---

# Raycasting
Roblox engine allows its users to cast an invisible ray from a [Vector3](https://developer.roblox.com/en-us/api-reference/datatype/Vector3) position towards a specified direction. Unlike normal rays, Roblox enables you to set the length of ray according to your needs. Using raycast, you can detect if the ray hits a [Basepart](https://developer.roblox.com/en-us/api-reference/class/BasePart) or [Terrain](https://developer.roblox.com/en-us/api-reference/class/Terrain).

## Casting A Ray
For casting a ray we use the method **`:Raycast()`** of worldroot ([workspace](https://developer.roblox.com/en-us/api-reference/class/Workspace)). **`Raycast()`** takes **three** arguments and returns [RaycastResult](https://developer.roblox.com/en-us/api-reference/datatype/RaycastResult)

* Origin            type: [Vector3](https://developer.roblox.com/en-us/api-reference/datatype/Vector3)
* Direction         type: [Vector3](https://developer.roblox.com/en-us/api-reference/datatype/Vector3)
* RaycastParams     type: [RaycastParams](https://developer.roblox.com/en-us/api-reference/datatype/RaycastParams)

```lua
local Raycast_result = workspace:Raycast(origin, direction, raycastparams)
```
<img src=https://github.com/Rodevs-Helpers/Helpers-Documents/blob/main/images/raycast1.png?raw=true width="500" height="500"/> 

### Origin
Origin of a ray is basically a [Vector3](https://developer.roblox.com/en-us/api-reference/datatype/Vector3) position of the world, from where the ray will start. 
We will take two [parts](https://developer.roblox.com/en-us/api-reference/class/Part). A red part and a green part and cast ray between them.

```lua
local origin = RedPart.Position
```
We have selected position of red part as origin for the ray.

### Direction
Direction is the [Vector3](https://developer.roblox.com/en-us/api-reference/datatype/Vector3) with a defined magnitude. Direction of a ray from a known destination (GreenPart.Position) can be easily calculated by using following formula

* Destination - Origin = Direction

If you are familiar with vectors then we are basically getting a [Vector3](https://developer.roblox.com/en-us/api-reference/datatype/Vector3) between the two positions. Once we have calculated the directional vector, we will adjust the length of it. For doing so we will get the unit vector of directional vector and multiply it with the number of studs (the length of ray in studs).

```lua
local direction = (GreenPart.Position - RedPart.Position).Unit * 100
```

In above example, the magnitude of ray is set to 100 studs.

### RaycastParams
[RaycastParams](https://developer.roblox.com/en-us/api-reference/datatype/RaycastParams) carries the parameters of `Raycast()`. It's property, `FilterDescendantsInstances` stores a table. It can be either a `Exclude` or `Include` depending on `FilterType`.

!!! note
    * `Enum.RaycastFilterType.Include` Every `BasePart` other than those given in filter list and their descendants will be ignored.
    * `Enum.RaycastFilterType.Exclude` Every `BasePart` other than those given in filter list and their descendants will be considered.
      
```lua
local RaycastParams = RaycastParams.new()
RaycastParams.FilterDescendantsInstances = {RedPart}
raycastParams.FilterType = Enum.RaycastFilterType.Exclude
```

In these params we have excluded the red part in order to prevent ray from being incident on the walls of red part.

Our overall code will be:

```lua
local origin = RedPart.Position
local direction = (GreenPart.Position - RedPart.Position).Unit * 100

local RaycastParams = RaycastParams.new()
RaycastParams.FilterDescendantsInstances = {RedPart}
raycastParams.FilterType = Enum.RaycastFilterType.Exclude

local Raycast_result = workspace:Raycast(origin, direction, raycastparams)
```

## RaycastResult
If the ray hits a basepart, it will return [RaycastResult](https://developer.roblox.com/en-us/api-reference/datatype/RaycastResult). It's properties carries result of raycast

* RaycastResult.Instance    | The BasePart intersected by the ray.
* RaycastResult.Position    | The world position where intersection took place.
* RaycastResult.Material    | The material of BasePart intersected by the ray.
* RaycastResult.Normal      | The vector perpendicular to the face of intersected surface.

```lua
local origin = RedPart.Position
local direction = (GreenPart.Position - RedPart.Position).Unit * 100

local RaycastParams = RaycastParams.new()
RaycastParams.FilterDescendantsInstances = {RedPart}
raycastParams.FilterType = Enum.RaycastFilterType.Exclude

local Raycast_result = workspace:Raycast(origin, direction, raycastparams)

print(Raycast_result.Position)
```

!!! warning
    `Raycast_result` will be `nil` if ray didn't hit any object.

<img src=https://github.com/Rodevs-Helpers/Helpers-Documents/blob/main/images/raycast2.png?raw=true width="500" height="500"/>

Now if we place another part between the two parts then ray will intersect the middle one and `Raycast_result` will carry properties related to  the yellow part.

## Closing!
As always, we hope you enjoyed reading and can utilize raycasting according to your needs. Whatever you are learning, please practice it on the spot. Just reading will not help you if you aren't practicing them.
In case of any mistakes, typos, etc please report the article!
