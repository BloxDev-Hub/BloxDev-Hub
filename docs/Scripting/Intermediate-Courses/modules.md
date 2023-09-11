---
title: What Is A Module Script?
template: docs.html
comments: true
hide:
  - navigation
---

# Module Scripts
What is a [ModuleScript](https://create.roblox.com/docs/education/coding-6/intro-to-module-scripts)?

A module script can host data such as a table, function, strings, and numbers. Anything. But, a Module Script can only **return** one data value.

Depending on what the module script is doing, handling server code/handling client code can go in **ServerScriptService** or **ReplicatedStorage**. Localized code for ReplicatedStorage and server code for ServerScriptService.

Module scripts will run code on the side they're called from if that makes sense. If you call a module script from a local script the module script will be running localized code. Thereby you would have access to the LocalPlayer.

## Why Use Module Scripts Over Normal Scripts
As a beginner, your main reason to use module scripts over normal scripts is for functions that you need to use in more than one script.
For example, giving a player coins each time they do something. Having a module script with a coin function that gives the Player coins.

Module scripts can also be useful to store data. If you have a Twitter code system you can store the codes in that module script with the number of coins they give.

## How Do You Use Module Scripts
Module scripts won't run any code unless you **require** them. So how do you require a module script? It's quite simple.
Firstly though, we're going to make a Module Script inside of ReplicatedStorage.


Inside of this, we're going to add a print when the module script is required and we're going to return a table.

```lua
local ModuleScript = {SalzuIsTheBest = 'SalzuIsTheBest'}

print('This module script has been required')

return ModuleScript
```

Then in a server script, we're going to require the module script. It will print "This module script has been required".

```lua
local ModuleScript = require(game.ReplicatedStorage.MyModuleScript) -- This module script has been required.
print(ModuleScript) -- SalzuIsTheBest
```

 We then print the module script returning a table with the value "SalzuIsTheBest"

### Adding Variables/Functions To Your Module Script

 Now we're going to talk about how to add variables to your Module Script. This isn't how you always might want to do it.

To add Values to a table you do:

```lua
Table.MyValue = 10
```

You can add functions like that too:

```lua
Table.Add = function(A,B)
    print(A+B)
end

--You can also add functions like this

function Table.Add(A,B)
    print(A+B)
end
```

### Scopes Within A Module Script

Module scripts work differently. You don't always want to make a function localized, why? If the function is localized then other scripts you require won't be able to run the function. 

Now, this doesn't mean putting local in front of a function inside of a module script. Any variable/function that the module script only uses should be localized.

Here I'll be showing right versus wrong.

Right:

```lua
function ModuleScript.Add(A,B)
    print(A+B)
end
```

Any script we require this module script in will be able to use that function.

Wrong:

```lua
local function ModuleScript.Add(A,B)
    print(A+B)
end
```

No other script will be able to use that function.

# Closing!
That's pretty much of it. Hope you enjoyed reading it. In case of any mistake, typos, etc. Please report the article. You can also give us reviews [here](https://docs.rodevs.com/Others/Help_Us%21/)
