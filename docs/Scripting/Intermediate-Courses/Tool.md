---
title: Scripting Tools
template: docs.html
comments: true
hide:
  - navigation
---
# Tools
As the name suggests, tools are the objects with which players can interact. Tools are equipped by the [Humanoid](https://developer.roblox.com/en-us/api-reference/class/Humanoid) of the player's character. Usually, tools are stored in the player's [Backpack](https://developer.roblox.com/en-us/api-reference/class/Backpack). When a tool is equipped, it is moved from [Backpack](https://developer.roblox.com/en-us/api-reference/class/Backpack) to the player's [Character](https://developer.roblox.com/en-us/api-reference/property/Player/Character). This means parenting a tool to the player's [Character](https://developer.roblox.com/en-us/api-reference/property/Player/Character) forces the character to equip it. However Roblox also offers methods [Humanoid:EquipTool()](https://developer.roblox.com/en-us/api-reference/function/Humanoid/EquipTool) and [Humanoid:UnequipTools()](https://developer.roblox.com/en-us/api-reference/function/Humanoid/UnequipTools) for this purpose.
Every tool requires a [BasePart](https://developer.roblox.com/en-us/api-reference/class/BasePart) named **Handle** as a child of it unless the property `Tool.RequiresHandle` is set to `false`.

## Creating A Tool
Add a part in the workspace. Change its shape and color to whatever you like. Name the part as **"Handle"**. Click the (+) icon next to workspace and add a **Tool** in it.

<img src=https://github.com/Rodevs-Helpers/Helpers-Documents/blob/main/images/Tool1.png?raw=true width="300" height="300"/>

Parent the **Handle** to the **Tool**.

<img src=https://github.com/Rodevs-Helpers/Helpers-Documents/blob/main/images/Tool2.png?raw=true width="300" height="300"/>

Now place tool inside [StarterPack](https://developer.roblox.com/en-us/api-reference/class/StarterPack).

<img src=https://github.com/Rodevs-Helpers/Helpers-Documents/blob/main/images/Tool3.png?raw=true width="300" height="300"/>

When the game runs, all the tools in [StarterPack](https://developer.roblox.com/en-us/api-reference/class/StarterPack) are replicated to the player's [Backpack](https://developer.roblox.com/en-us/api-reference/class/Backpack).

Now, if you run the game, you can see a tool in your inventory.

<img src=https://github.com/Rodevs-Helpers/Helpers-Documents/blob/main/images/Tool4.png?raw=true width="500" height="500"/>

## Setting Grips
the grip of a tool can be adjusted by changing the following properties:

<img src=https://github.com/Rodevs-Helpers/Helpers-Documents/blob/main/images/Tool5.png?raw=true width="300" height="300"/>

However there is an amazing plugin, you can use for adjusting grips

[Tool Grip Editor](https://www.roblox.com/library/174577307/Tool-Grip-Editor){ .md-button .md-button--primary }

<img src=https://github.com/Rodevs-Helpers/Helpers-Documents/blob/main/images/Tool6.png?raw=true width="500" height="500"/>

## Scripting Tool

As most of the objects, a tool can be fully utilized by scripting it. Insert a [LocalScript](https://developer.roblox.com/en-us/api-reference/class/LocalScript) in the tool.

When a tool is equipped, the event [Equipped](https://developer.roblox.com/en-us/api-reference/event/Tool/Equipped) is fired.
Example Code:

```lua
script.Parent.Equipped:Connect(function()
    print("Tool got equipped")
end)
```

???+ note
    * `script` is a Roblox global which carries the reference of current [Script](https://developer.roblox.com/en-us/api-reference/class/Script) or [LocalScript](https://developer.roblox.com/en-us/api-reference/class/LocalScript).
    * Equipped event returns `Mouse` object. Because it is deprecated, we will not cover it in this guide.

Similarly, [Tool.Unequipped](https://developer.roblox.com/en-us/api-reference/event/Tool/Unequipped) is fired.
Example Code:

```lua
script.Parent.Unequipped:Connect(function()
    print("Tool got unequipped")
end)
```

It is not just limited to equipped and unequipped. Roblox engine also offers [Activated](https://developer.roblox.com/en-us/api-reference/event/Tool/Activated) and [Deactivated](https://developer.roblox.com/en-us/api-reference/event/Tool/Deactivated) which are fired when a player activates (click/tap while the tool is equipped) and deactivates (left mouse button is released) respectively.
Example Code:

```lua
script.Parent.Activated:Connect(function()
    print("Tool is being used")
end)

script.Parent.Deactivated:Connect(function()
    print("Tool is no longer being used")
end)
```

These are the only events of tools other than those inherited from `instance`.

# Additionals

* [Roblox's Offical Api Refernce Of Tools](https://developer.roblox.com/en-us/api-reference/class/Tool)


# Closing!
That's pretty much of it. Hope you enjoyed reading it. In case of any mistake, typos, etc. Please report the article. You can also give us reviews [here](https://rodevs-helpers.github.io/Helpers-Documents/Others/Help_Us%21/)