---
Title: Scripts and Local scripts
---

#Script
Script is an object that contains Lua code. It is executed only when its ancestor is either [Workspcase](https://developer.roblox.com/en-us/api-reference/class/Workspace) or [ServerScriptService](https://developer.roblox.com/en-us/api-reference/class/ServerScriptService). It can also run if it's parent property is set to nil.
Normally a script is used for server-side code execution. It has excess to almost all the objects, properties of data model.

In order to insert a script, click the `+` icon next to the desired instance in explorer window. Every script by default has a command 
```lua
print("Hello World!")
```
# Local Scripts
Local script also carries Lua code however they are used for client-side code execution. Local scripts only run when they are descendant of any of the following objects:

* [PlayerScripts](https://developer.roblox.com/en-us/api-reference/class/PlayerScripts)
* [Backpack](https://developer.roblox.com/en-us/api-reference/class/Backpack)
* [PlayerGui](https://developer.roblox.com/en-us/api-reference/class/PlayerGui)
* [Character](https://developer.roblox.com/en-us/api-reference/property/Player/Character)
* [ReplicatedFirst](https://developer.roblox.com/en-us/api-reference/class/ReplicatedFirst)

!!! note ""
    Basically when local script is placed in any of them, it is replicated to every player. This means local script runs on every client separately and every client has their own local scripts.

Mainly local scripts are used to access client only objects such as input, camera, etc. Essentially local  scripts are able to access the client running them by using `LocalPlayer` property of [Players](https://developer.roblox.com/en-us/api-reference/class/Players). 

Local script can be added in the same way as normal script.

# Closing!
I hope, now you have a basic understanding of local script and a normal script. If you find any typos, or any sort of flaws then please report it [here](https://rodevs-helpers.github.io/Helpers-Documents/Others/Help_Us%21/)