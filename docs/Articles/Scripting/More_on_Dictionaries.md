---
title: More on Dictionaries
---

# For real? There's more?
...Yes. The ROBLOX API actually uses dictionaries far more often than you'd imagine. This is what I will be going through in this article.

To progress on however, you are expected to have a basic understanding of tables and sufficient experience with at least `for` loops. You can read them up with the tables guide in the Lua Learning section!

## The Beginning
Recall how to get a value from a dictionary:
```lua
local dictionary = 
	{
		["One"] = 1,
		["Two"] = 2,
		["Three"] = 3,
		["Four"] = 4,
		["Five"] = 5
	}

print(dictionary["One"])

-- Output:
-- 1
```

This should look very familiar to you if you've used dictionaries for even a short length of time. 

However, what if I told you there's another way to access a value in a dictionary? Watch this demonstration.

```lua
local dictionary = 
	{
		["One"] = 1,
		["Two"] = 2,
		["Three"] = 3,
		["Four"] = 4,
		["Five"] = 5
	}

print(dictionary.One)

-- Output:
-- 1
```

That's right! You can actually access a dictionary's value just by using `.` followed by the key name.
Hold onto this - while this alone may seem like an unnecessary feature, this article will build on top of this concept. I will cover exactly why this can be useful.

## Explorer as a Dictionary
If you're new to this concept, you might want to hold onto your chair tight and hope you don't get blown back far into your seat:

> *The game is really just a massive dictionary.*

That's right, it actually is! Remember the demonstration we just did? Now compare it to this:

```lua
-- print(dictionary.One)
print(workspace.Baseplate.Name) -- workspace is a global namespace for the Workspace object.

-- Output:
-- Baseplate
```

Do you see the similarity? Let's apply what we learnt earlier on and see if it works:

```lua
-- print(dictionary["One"])
print(workspace["Baseplate"].Name)

-- Output:
-- Baseplate
```

This is what I meant! The game is really just a massive dictionary where the objects are the keys, and the instances are the values! 

In summary, you can get an object with either of these two ways in consideration that the game is a dictionary!

```lua
print(workspace.Baseplate.Name)
print(workspace["Baseplate"].Name)

-- Both will return "Baseplate".
```

This is cool, isn't it? But hold on, there's more.

## Properties as a Dictionary
Let's use the example from before:
```lua
print(workspace.Baseplate.Name)
print(workspace["Baseplate"].Name)
```

Now here's another shocker:

> *An object is really just another massive dictionary.*

Yes! Using the same few demonstrations above, we can call the property of an object like as if it was part of a dictionary:

```lua
print(workspace.Baseplate.Name)
print(workspace.Baseplate["Name"])

-- Both will return "Baseplate".
```

## Setting properties with loops
One of the biggest uses of such a feature is that you can set the properties of an object by using a loop. Let's take a look at the typical approach that you might instinctively use:

```lua
local name = "PartName"
local material = Enum.Material.SmoothPlastic
local position = Vector3.new(0, 0, 0)
local size = Vector3.new(1, 1, 1) }

workspace.Baseplate.Name = name
workspace.Baseplate.Material = material
workspace.Baseplate.Position = position
workspace.Baseplate.Size = size
```

While this could work, it is not very scalable - not only do you have to store lots of variables, code like this can get very difficult to edit especially when you have lots of properties to change. Fret not, we can change all that using property dictionaries and a generic `for` loop.

```lua
local propertyDictionary = 
    {
        -- ["Property Name"] = "Value"
        ["Name"] = "PartName",
        ["Material"] = Enum.Material.SmoothPlastic,
        ["Position"] = Vector3.new(0, 0, 0),
        ["Size"] = Vector3.new(1, 1, 1) },
    }

for property, value in pairs(propertyDictionary) do
    workspace.Baseplate[property] = value
end
```

This looks much better now, doesn't it? Not only will your properties be set no matter how many of them you wish to change, you know exactly where to look if you want to change the value of a property! 

Things like this really add up when you have multiple parts to change the properties of:

```lua
local parts = { workspace.Part1, workspace.Part2, workspace.Part3 }
local propertyDictionary = 
    {
        -- ["Property Name"] = "Value"
        ["Name"] = "PartName",
        ["Material"] = Enum.Material.SmoothPlastic,
        ["Position"] = Vector3.new(0, 0, 0),
        ["Size"] = Vector3.new(1, 1, 1) },
    }

for index, part in ipairs(parts) do
    for property, value in pairs(propertyDictionary) do
        part[property] = value
    end
end
```

Undoubtedly, this looks way cleaner than our initial approach. Not only that, because we stored our property values in an easy-to-access table, we know exactly where to look when we need to edit a property for our parts in the future!

**Do make sure to provide the correct property name for your keys however. Otherwise, your script may throw a nil error!**

## Closing
Have a suggestion to improve any of the two articles? Ping me on Discord! @valkyria#0001