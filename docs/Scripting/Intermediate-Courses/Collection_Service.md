---
title: Collection Service
template: docs.html
comments: true
hide:
  - navigation
---

# Collection Service in Roblox Studio
The Collection Service is a built-in service in Roblox Studio that provides a way to manage and manipulate groups of objects in a game. It is a powerful tool that can be used to organize game objects and trigger events when certain conditions are met. In this document, we will explore some of the methods and use cases of the Collection Service.

## Creating Collections
To create a Collection, you need to first tag the objects that you want to include in the collection. Tags are simply string names that are associated with objects in the game. You can add a tag to an object using the `CollectionService:AddTag()` method.

Consider we have two models in the workspace, namely "Enemy1" and "Enemy2". We can tag them with "Enemies".

```lua
local CollectionService = game:GetService("CollectionService")
local Enemy1 = workspace.Enemy1
local Enemy2 = workspace.Enemy2

-- Add a "Enemies" tag to enemy1 and enemy2
CollectionService:AddTag(Enemy1, "Enemies")
CollectionService:AddTag(Enemy2, "Enemies")
```

## Accessing Objects in a Collection
Once you have tagged the objects, you can access the objects in it using standard Lua table indexing syntax using the `CollectionService:GetTagged() method. `

```lua
-- Retrieve all objects tagged with "Enemies"
local Enemies = CollectionService:GetTagged("Enemies")
```
This will return a group of all objects in the game that have been tagged with "Enemies".

Now, you can access a particular member by indexing the returned table

```lua
local Enemy1 = Enemies[1]
```

You can also use a for loop to iterate over all the objects in the Collection:

```lua
for _, Enemy in ipairs(Enemies) do
    -- Do something with each enemy
end
```

## Example Usecase
### Using Collections for Spawning Objects
One of the most simple use cases for the Collection Service is to spawn objects in the game. To do this, you first need to create a Collection of spawn points. You can tag the spawn points with a specific tag, such as "SpawnPoint".

```lua
local Spawn1 = workspace.Spawn1
local Spawn2 = workspace.Spawn2
local Spawn3 = workspace.Spawn3 
-- Add a "SpawnPoint" tag to each spawn point 
CollectionService:AddTag(Spawn1, "SpawnPoint") 
CollectionService:AddTag(Spawn2, "SpawnPoint") 
CollectionService:AddTag(Spawn3, "SpawnPoint")
```

You can then retrieve all the spawn points using the `CollectionService:GetTagged()` method:

```lua
local SpawnPoints = CollectionService:GetTagged("SpawnPoint")
```

To spawn an object at a random spawn point, you can use the following code:

```lua
-- Choose a random spawn point
local SpawnPoint = SpawnPoints[math.random(1, #SpawnPoint)]

-- Clone the object and set its position to the spawn point
local Object = game:GetService("ServerStorage"):FindFirstChild("Enemy"):Clone()
Object.Parent = workspace
Object.Position = SpawnPoint.Position
```

### Using Collections for Triggering Events
Another use case for the Collection Service is to trigger events when certain conditions are met. For example, you might want to trigger an event when a player picks up all the items in a Collection. To do this, you can listen for changes to the Collection using the `CollectionService:GetInstanceAddedSignal()` method.

```lua
local items = CollectionService:GetTagged("Items")

-- Listen for changes to the "Items" Collection
local connection = CollectionService:GetInstanceAddedSignal("Items"):Connect(function(item)
    local ItemsRemaining = #CollectionService:GetTagged("Items")
    if ItemsRemaining == 0 then 
        print("You collected all the items!") 
    end 
end)
```
This code will listen for new objects being added to the "Items" Collection. When a new object is added, it will check how many items are remaining in the Collection. If there are no items remaining, it will print a message to the console. ## Using Collections for Cleanup Finally, you can use the Collection Service for cleaning up objects in the game. For example, you might want to delete all the enemies in a game when the player completes a level. To do this, you can create a Collection of all the enemies and then delete them using the `Destroy()` method.

```lua
local enemies = CollectionService:GetTagged("Enemies")
-- Delete all enemies 
for _, enemy in ipairs(enemies) do 
        enemy:Destroy() 
end
```

## Conclusion
The Collection Service is a powerful tool for managing and manipulating groups of objects in a game. It can be used for spawning objects, triggering events, and cleaning up objects. By using the Collection Service, you can create more organized and efficient games.

You may think, "Can I just make a table?", "I don't need it", "Useless service". This is just a preference of the scripter, what they like or not. You might or might not find it useful for yourself but I have seen some do, yet it's better to have a knowledge of what it is because it won't hurt and you never know what you will need in future.