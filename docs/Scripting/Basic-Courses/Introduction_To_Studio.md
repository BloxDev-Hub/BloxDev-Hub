---
title: Introduction To Studio
template: docs.html
comments: true
hide:
  - navigation
---

# Studio
Roblox studio is used for developing games in Roblox. It has lots of cool features and stuff and is one of the best game engines.

**[Downloading Studio](https://www.roblox.com/create)**
## Setting up studio
First of all, you need to set up your studio. 
### Explorer
Explorer window displays every object inside the data model in a tree structure. Here is how it looks like

![Explorer](https://imgur.com/cdEHjFw.png)

It is enabled by default but if you ever need to disable/enable it, you can from the view tab on the top bar.

![viewtab](https://imgur.com/CicwqfX.png)

### Properties
The properties window displays all the visible properties of the selected object. It can be enabled from the view tab on the top bar.

![property](https://imgur.com/TyPtC7x.png)

In the above picture, it is displaying properties of a part named **Baseplate**. It is an important part of the studio and you will always need it whenever you have to change the property of an object manually.

### Output Window
The output window is basically a window that displays, anything you print, warnings, errors, and other messages of such sorts. You can enable it from the top bar. Click the **view** tab and select **output**.

![viewtab](https://imgur.com/CicwqfX.png)

![output](https://imgur.com/eEFePUJ.png)


## Introduction To Scripting.
Scripting is an essential part of Roblox development. To get optimum benefit of Roblox's services, instances, etc you would require scripting. In fact, you can not make a game in Roblox without scripting it.
Roblox engine uses Luau for scripting, a modified version of Lua. Like almost all high-level languages, the fundamentals of Lua are pretty easy to learn. Now, let's go through some elemental stuff regarding Roblox scripting.

### Adding Scripts
To add a script inside of any of the objects, click the ![eh](https://imgur.com/u8wosCv.png) icon, next to that object in the explorer window. As an example, we have added a script in "ServerScriptService".

![script](https://imgur.com/pQFndei.png)

This is how we can add a script.

#### Printing.
`print()` is a Lua global, mainly used for debugging. In the studio, when you print something it is displayed on the output window.
As an example use, we will print the sum of two numbers.

```lua
print(17 + 19)
```

You can see the output on the output window.

![print](https://imgur.com/cmGeY6E.png)

## Closing!
That's pretty much of it. Hope you enjoyed reading it. In case of any mistake, typos, etc. Please report the article. You can also give us reviews [here](https://rodevs-helpers.github.io/Helpers-Documents/Others/Help_Us%21/)