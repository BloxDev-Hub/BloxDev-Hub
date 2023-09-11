---
title: Intoduction To Selection And Highlights
template: docs.html
comments: true
hide:
  - navigation
---
# Selection And Highlights

**Selection Boxes/Spheres** and **Highlights** are objects that you can use in your game for multiple purposes. These objects add a boundary over other parts/models. Let's try to use them.

## Selection Box
The selection box renders a box over a part or model. You must have seen this in many games where it's used to prominent selected objects. 

![select1](https://imgur.com/O7QyOLd.png)

It is very simple and very easy to create one.

Add a part in **Workspace** and a script in **ServerScriptService**

![explorer](https://imgur.com/1A0jopv.png)

In our script, we will create a selection box. Parent the selection box to the art and set **Adornee** property to part.

```lua
local part = workspace.Part

local selectionbox = Instance.new("SelectionBox")
selectionbox.Parent = part
selectionbox.Adornee = part
```

We got a nice selection box over our part

![selectionbox1](https://imgur.com/ZVAMTMy.png)

Now you may wish to change the color of the selection box. For doing so, we will change the `Color3` property of selection box.

Our code will be

```lua
local part = workspace.Part

local selectionbox = Instance.new("SelectionBox")
selectionbox.Parent = part
selectionbox.Adornee = part
selectionbox.Color3 = Color3.new(1, 1, 0)
```

We have changed the color to yellow

![yellowselectionbox](.png)

The selection box also allows you to change its thickness. It can be done by changing the `LineThickness` property.

```lua
local part = workspace.Part

local selectionbox = Instance.new("SelectionBox")
selectionbox.Parent = part
selectionbox.Adornee = part
selectionbox.Color3 = Color3.new(1, 1, 0)
selectionbox.LineThickness = 0.09
```

Now, if you compare it with the one we created earlier, you can see the difference. 

## Selection Sphere
Selection spheres are the same as selection boxes except the shape is a sphere. The way of using is almost the same as in the selection box.

```lua
local part = workspace.Part

local selectionbox = Instance.new("SelectionSphere")
selectionbox.Parent = part
selectionbox.Adornee = part
selectionbox.Color3 = Color3.new(1, 1, 0)
selectionbox.LineThickness = 0.09
```

![sphere](https://imgur.com/sIDJtiu.png)

You might be thinking, how is it a sphere? Lower the transparency of part and you can see the sphere.

![visiblesphere](https://imgur.com/nEWHls3.png)

## Highlight
As the name suggests, it is an object you can use for highlighting objects. It can be utilized in many aspects. Let's look forward to how we can use it.

We will use a rig and highlight it. For doing so we will create a highlight object, parent it to the rig model, and lastly set its adornee to that model.

```lua
local dummy = workspace.Dummy

local highlight = Instance.new("Highlight")
highlight.Parent = dummy

```

We have highlighted the rig and it's quite cool. 

![highlight1](https://imgur.com/apY2tlI.png)

Its most interesting feature is that you can see the highlighted object through other base parts.

![behind](.png)

Highlights allow you to change the outline color as well as the fill color. It can be done by changing `OutlineColor` and `FillColor` properties respectively. 

```lua
local dummy = workspace.Dummy

local highlight = Instance.new("Highlight")
highlight.Parent = dummy
highlight.Adornee = dummy
highlight.OutlineColor = Color3.new(0, 0, 1)
highlight.FillColor = Color3.new(0, 0, 0)
```

![color](https://imgur.com/0e3rAnr.png)

You can also remove the fill color by changing the `FillTransparency` property.

```lua
local dummy = workspace.Dummy

local highlight = Instance.new("Highlight")
highlight.Parent = dummy
highlight.Adornee = dummy
highlight.OutlineColor = Color3.new(1, 0, 0.498039)
highlight.FillTransparency = 1
```

And here we go.

![fillgone](https://imgur.com/m2O33Qk.png)

# Closing!
I hope you learned something new and can use it in your game. Thanks a lot for reading! Happy developing!