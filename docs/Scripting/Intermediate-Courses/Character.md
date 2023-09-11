---
title: Player's Character
template: docs.html
comments: true
hide:
  - navigation
---

# Character
The Character is the physical 3d model of your [Player](https://create.roblox.com/docs/reference/engine/classes/Player).

## How Do You Access The Character
Depending if you're on the [Client/Server](https://developer.roblox.com/en-us/articles/Roblox-Client-Server-Model) the character can be accessed in two different ways.

Client:
```lua
local Players = game:GetService('Players')
local Player = Players.LocalPlayer
local Character = Player.Character or Player.CharacterAdded:Wait()
print(Character.Name) -- TheSalzu
```

Just to clear up some confusion, the reason we do Player.CharacterAdded:Wait() is because the player's character may not have fully loaded in yet. If you're also confused about the Players service refer to [Players](https://developer.roblox.com/en-us/api-reference/class/Players)

Now if you're on the server this is a way you can access the character

```lua
local Players = game:GetService('Players')
    Players.PlayerAdded:Connect(function(Player)
        Player.CharacterAdded:Connect(function(Character)
            print(Character.Name) -- TheSalzu
    end)
end)
```

Now, this isn't how you're always going to access a Character, they're plenty of ways to get the character.

### More Ways To Access The Character
If you're using a tool and want to get the Character then you can do

```lua
local Tool = ToolInstance

Tool.Activated:Connect(function()
    local Character = Tool.Parent -- Tools always get parented to the Character

    print(Character.Name) -- TheSalzu
end)
```

A general way to get the character is by checking if it has a HumanoidRootPart. For this, we'll be using a part getting touched.

```lua
local Part = workspace.Part -- Example

Part.Touched:Connect(function(PartThatGotTouched)
    local HumanoidRootPart = PartThatGotTouched.Parent:FindFirstChild('HumanoidRootPart')

    if HumanoidRootPart then
        print('We found a character!')
    end
end)
```

One last thing that isn't really related to getting the character but is still useful is, getting the player from the character.

```lua
local Players = game:GetService('Players')
local Player = Players:GetPlayerFromCharacter(CharacterModel)
print(Player) -- TheSalzu
```


## Humanoid
The [Humanoid](https://create.roblox.com/docs/reference/engine/classes/Humanoid) is what gives the Character model functionality. It lets the Character move, jump, and interact. The humanoid will always be parented under the character and it has to be named "Humanoid". If it isn't named Humanoid then your reset button will not work.

Cool things you can do with the humanoid:

![humanoid](https://imgur.com/ltzzVda.png)

As you can see from the image above, the humanoid has a lot of things you can do with it. I will list some here.

```lua
local Humanoid = Character.Humanoid
Humanoid.Health = 1000
Humanoid.MaxHealth = 1000
Humanoid.JumpPower = 100
Humanoid.WalkSpeed = 60
Humanoid.AutoJumpEnabled = true/false -- On mobile when you hit an obstacle it will auto jump
Humanoid.DisplayName = 'String'
```

These are the fun ones that you can mess with but now I'll talk about some useful methods the Humanoid has.
These are not all of the methods the humanoid has!

```lua
local Humanoid = Character.Humanoid

Humanoid:EquipTool(ToolInstance)
Humanoid:UnEquipTools()
Humanoid:TakeDamage(Number)
Humanoid:AddAccessory(AccessoryInstance)
Humanoid:ChangeState(Enum.State.YourState) --Walking,Running,Ragdoll,Sitting,Jumping
Humanoid:GetAccessories() -- Returns an array of all of the accessories
Humanoid:GetState() -- Returns the current state
Humanoid:PlayEmote('EmoteName')
```

Now we can talk about some useful events the humanoid has

```lua
local Humanoid = Character.Humanoid

Humanoid.Died:Connect(function()
    print('The humanoid has died!')
end)

Humanoid.HealthChanged:Connect(function(Health)
    print('The health has changed!')
end)

Humanoid.StateChanged:Connect(function(State)
    print(State)
end)

-- Here are some state changes, for these, I will not be doing the full event with the end)

Humanoid.Jumping:Connect(function())
Humanoid.Running:Connect(function())
Humanoid.Swimming:Connect(function())
Humanoid.Seated:Connect(function())
Humanoid.Ragdoll:Connect(function())
Humanoid.FreeFalling:Connect(function())
```

That's all for the Humanoid. If you want to know more go take a good read at:

[Humanoid API](https://create.roblox.com/docs/reference/engine/classes/Humanoid)

## How To Move A Character
Moving a character is quite simple. All you have to do is simply change their Pivot via CFrame.

```lua
local Character -- Your method of getting the Character

Character:PivotTo(CFrameValue)
```

For more information on CFrame go take a read at:

[Roblox's official guide on CFrame](https://developer.roblox.com/en-us/articles/Understanding-CFrame)  

## Closing!
That's pretty much of it. Hope you enjoyed reading it. In case of any mistake, typos, etc. Please report the article. You can also give us reviews [here](https://rodevs-helpers.github.io/Helpers-Documents/Others/Help_Us%21/)
