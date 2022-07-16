---
Title: Creating Leaderstats
---

# Leaderstats
Leaderstat/Leaderboard is basically the board that appears on the right top of player's screen. if you are used to playing games on Roblox then you must have seen this in many games.

<img src=https://github.com/Rodevs-Helpers/Helpers-Documents/blob/editing/images/leaderstats1.png?raw=true width="500" height="500"/>

## How to create one?
Making a leaderstats is pretty simple. First of all we will add a **script** in [ServerScriptService](https://developer.roblox.com/en-us/api-reference/class/ServerScriptService).

<img src=https://github.com/Rodevs-Helpers/Helpers-Documents/blob/editing/images/leaderstats2.png?raw=true width="500" height="500"/>

For making leaderstats, we basically have to add a folder inside every player and name it **leaderstats**. Once made the folder, we will add value objects such as [IntValue](https://developer.roblox.com/en-us/api-reference/class/IntValue), [NumberValue](https://developer.roblox.com/en-us/api-reference/class/NumberValue), [StringValue](https://developer.roblox.com/en-us/api-reference/class/StringValue) etc.

In script we will get every player that joins the game and create leaderstats for it. In order to get player we will connect a function to [PlayerAdded](https://developer.roblox.com/en-us/api-reference/event/Players/PlayerAdded). In the function we will create the folder for leaderstats and set values inside it.

```lua
local function stats_handler(player)
    local leaderstats = Instance.new("Folder")
	leaderstats.Name = "leaderstats"
	leaderstats.Parent = player

    local points = Instance.new("IntValue")
	points.Name = "Points"
	points.Parent = leaderstats
end

game.Players.PlayerAdded:Connect(stats_handler)
```

In the first part of `stats_handler` we created a folder using [instance.new()](https://developer.roblox.com/en-us/api-reference/class/Instance) and named it **leaderstats** and lastly parented it to the [Player](https://developer.roblox.com/en-us/api-reference/class/Player). The `player` was returned by [PlayerAdded](https://developer.roblox.com/en-us/api-reference/event/Players/PlayerAdded).
In second part, we created an [IntValue](https://developer.roblox.com/en-us/api-reference/class/IntValue), named it "Points" and set its parent to the `leaderstats` folder.

Now, if you press `f5` to run the game. You can see leaderstats on your screen.

!!! caution
    The folder must be exactly named as **leaderstats**. In case of any misspelling or capitalizing, Roblox engine will not create the leaderboard.

## Setting Values
Once created leaderstats you can set values by changing the `Value` property of [IntValue](https://developer.roblox.com/en-us/api-reference/class/IntValue). 

```lua
local function stats_handler(player)
    local leaderstats = Instance.new("Folder")
	leaderstats.Name = "leaderstats"
	leaderstats.Parent = player

    local points = Instance.new("IntValue")
	points.Name = "Points"
	points.Parent = leaderstats
    points.Value = 100
end

game.Players.PlayerAdded:Connect(stats_handler)
```

No, if you run the game. Your points will be `100`.

## Implementing
As an example usage. Create a part in workspace and add [ClickDetector](https://developer.roblox.com/en-us/api-reference/class/ClickDetector) in it. You can either make a seperate script or use the ordinary one.
We will use [MouseClick](https://developer.roblox.com/en-us/api-reference/event/ClickDetector/MouseClick) event of [ClickDetector](https://developer.roblox.com/en-us/api-reference/class/ClickDetector) which is fired whenever a player interacts with it. This event also returns that [Player](https://developer.roblox.com/en-us/api-reference/class/Player).

<img src=https://github.com/Rodevs-Helpers/Helpers-Documents/blob/main/images/leaderstats3.png?raw=true width="500" height="500"/>

```lua
workspace.Part.ClickDetector.MouseClick:Connect(function(player)
	player.leaderstats.Value = player.leaderstats.Points.Value + 1
end)
```
Now every time you click the part. It will increase your points by 1

## Closing!
As always, we hope you enjoyed reading and can utilize leaderstats according to your needs. Whatever you are learning, please practice it on the spot. Just reading will not help you if you aren't practicing them.
In case of any mistakes, typos, etc please report the article!
