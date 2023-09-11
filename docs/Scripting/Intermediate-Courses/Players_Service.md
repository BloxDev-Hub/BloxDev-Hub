---
title: Introduction To Players Service
template: docs.html
comments: true
hide:
  - navigation
---

# Players Service
Hey! In this article, you'll learn how to use the [**Players Service**](https://create.roblox.com/docs/reference/engine/classes/Players).
Before we begin, make sure you understand the basics of Roblox Scripting. You could start [**here**](https://rodevs-helpers.github.io/Helpers-Documents/Lua-Learning/basic-loops/).
This tutorial may not cover all of the Players service, but only the most frequently used parts!

## What is the Players Service?
The Players service is a service that contains all the players who are presently connecting their clients to a Roblox game server. You can access things such as a player's friends, avatar, username, etc.


## Basic Events

### PlayerAdded
This event fires when a player enters the game.

#### Basic Usage
```lua
local Players = game:GetService("Players")

Players.PlayerAdded:Connect(function(player)
	print(player.Name .." has joined the game!")
end)
```
In the first line, we assign the Players service to a variable ``Players``. In the third line we use the PlayerAdded event, which gets us the player that is joining when the event was fired. And then, we print out the player's name!

!!! note " "
	PlayerAdded sometimes doesn't properly function in solo mode i.e in Roblox Studio.

### PlayerRemoving
This event is very similar to PlayerAdded, except it fires when a player leaves the game.

#### Basic Usage
```lua
local Players = game:GetService("Players")

Players.PlayerRemoving:Connect(function(player)
	print(player.Name .."has left the game!")
end)
```

## Basic Methods

### GetPlayers
This method returns an array of player(s) that are currently in the server at the time of calling this method.

#### Basic Usage
```lua
Players = game:GetService("Players")
for i, player in ipairs(Players:GetPlayers()) do
    print(player.Name)
end
```
The following code will print all of the players' names that are currently on the server at the time.


#### GetPlayerFromCharacter
This method returns the player associated with the given character, or nil if one cannot be found.

#### Basic Usage
```lua
local Players = game:GetService("Players")

local character = workspace.Player --the character of a player. Change the "Player" to your username.
local player = Players:GetPlayerFromCharacter(character)
```

### GetPlayerByUserId
This method returns the player who has the given UserId in the server.

#### Basic Usage
```lua
local Players = game:GetService("Players")

local player = Players:GetPlayerByUserId(123)  
```
This will return the player with the given UserId if they are on the server, or else it will return nil.
