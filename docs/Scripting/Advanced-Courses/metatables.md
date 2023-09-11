---
title: Metatables
template: docs.html
comments: true
hide:
  - navigation
---

 [1]: https://developer.roblox.com/en-us/articles/Metatables
 [2]: https://devforum.roblox.com/t/all-you-need-to-know-about-metatables-and-metamethods/503259

## Pre-requisites
Before reading this tutorial, you should know about tables.
An explanation of tables exists in the Lua-Learning folder.

# What's a metatable?
Metatables allow tables to become more powerful. Any table can have a metatable and
they can hold metamethods, which are similar to events. I like to call them table-events.

## Use cases for metatables
Metatables are often used to simulate Object Oriented Programming, but aren't essential to that. 

## Using setmetatable()
setmetatable() is a global function by Lua that you can use to set a metatable to a table.
It takes in the table as the first argument and the metatable as the second.

```lua
local normalTable = {}
local metaTable = {}

setmetatable(normalTable, metaTable) --metaTable is the metatable of our normalTable now!
```

setmetatable() also returns the table the metatable was set to, we don't really need it in this example though.

**Common misunderstanding:** Often, people think that the table becomes the metatable. That isn't true.
Instead, imagine the metatable as an addition to the table.

## Explanation of metamethods using __index
The power of metatables comes from their metamethods. You can see a list of all the metamethods [here][1].
We will be using __index now.
__index fires, when nil is indexed in our table. We could set __index to another table for example and it would search through that.

```lua
local fruits = {
    Apple = "red",
    Banana = "yellow",
    Orange = "orange"
}
local normalTable = {}
local metaTable = {}
metaTable.__index = fruits
setmetatable(normalTable, metaTable)

print(normalTable.Apple) --> red
```

The reason this prints out red is because our __index metamethod leads it to our fruits dictionary.
Here a visualization of what is happening:

normalTable.Apple --> nil --> does the table have a metatable? Yes --> does that metatable have an __index
metamethod? Yes --> use that to return a value.

We could also store the fruits inside of our metaTable, we would just have to set our __index to our metatable.

```lua
local normalTable = {}
local metaTable = { 
    Apple = "red",
    Banana = "yellow",
    Orange = "orange"
}
metaTable.__index = metaTable
setmetatable(normalTable, metaTable)

print(normalTable.Apple) --> red
```

A metatable can have many different metamethods, it isn't limited to one.
Let's set our index to a function and see what happens!

```lua
local normalTable = {}
local metaTable = {}
metaTable.__index = function()
    print("Tried to index nil!")
end
setmetatable(normalTable, metaTable)

local value = normalTable.Apple --> Tried to index nil!
```

You can also return something inside of the function.

```lua
local normalTable = {}
local metaTable = {}
metaTable.__index = function()
    return "Tried to index nil!"
end
setmetatable(normalTable, metaTable)

print(normalTable.Apple) --> Tried to index nil!
```

Apart from that, __index and most of the other metamethods also pass parameters.
__index passes the table that's trying to be indexed and the index that was not found.

```lua
local normalTable = {}
local metaTable = {}
metaTable.__index = function(indexedTable, invalidIndex)
    return "Tried to index " .. invalidIndex .. " inside of " .. tostring(indexedTable) --tostring so it doesn't error
end
setmetatable(normalTable, metaTable)

print(normalTable.Apple) --> Tried to index Apple inside of table: 0x8e801614244a0fbb
```

As far as I know though, setting a function to __index is quite expensive.

## Changed event for tables using __newindex
Now that we roughly know about metatables and metamethods, we can try scripting a Changed event for tables and learn about a new metamethod: __newindex
__newindex fires, whenever you are trying to set a new value in a table:

```lua
local normalTable = {}
local metaTable = {}
metaTable.__newindex = function()
    print("Trying to set a new value")
end
setmetatable(normalTable, metaTable)

normalTable.Apple = "red" --> Trying to set a new value
```

It actually stops it from setting Apple to red, so trying to print normalTable.Apple will return nil, or if you have an __index metamethod, fire that.

The problem with this is, that it doesn't account for changes, only new values being set.
The most common workaround probably is making a table that is empty, and inside of the function, change our actual table's values:

```lua
local realTable = {
    Money = 5
}
local emptyTable = {}
local metaTable = {}
metaTable.__newindex = function(table, index, value)
    print("Trying to set a new value")
end
setmetatable(emptyTable, metaTable)
```

__newindex passes the table, index and value as parameters. We don't really care about the table because we already know it's emptyTable, we only care about the index and value.

We will check if in our realTable, setting index to value would be a change, and if so, print out "changed"

```lua
local realTable = {
    Money = 5
}
local emptyTable = {}
local metaTable = {}
metaTable.__newindex = function(table, index, value)
    if realTable[index] ~= value then
        realTable[index] = value
        print("Changed")
    end
end
setmetatable(emptyTable, metaTable)
```

We also have to set index to the value in our realTable.
With that, we've scripted a Changed event for tables!

## Thanks for reading!
There is much more to metatables, of course, I didn't want this tutorial to be too long.
If you want to learn more about them, I recommend these tutorials:
[DevHub's article on metatables][1]
[Starmaq's tutorial on DevForum][2]