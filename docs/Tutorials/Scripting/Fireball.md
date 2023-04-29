---
title: Making Shootable Fireballs
description: Learn to make shooting fire balls in roblox studio!
og_image: https://imgur.com/dgw1giK.png
---

In this tutorial, I will be showing you how to make a fireball shooting system. Before starting, keep in your mind that primarily this guide is supposed to give you concepts that you can utilize in your game. If you are willing to copy everything, then you are likely to face issues and might find it unsuitable for your game. This tutorial requires you to have basic knowledge of roblox scripting. Now let's begin!

# Setting Up

## Making Fireball
Add a sphere in the workspace. This sphere will be our fireball. We will name it "Fire_Ball". Set the size of the ball to something that looks good to you. Set the transparency of the ball to `1`. Now, add a **Fire** object in the ball. In the property window, set the heat to 0 to make it look like an actual fireball, not an object having fired on it.

=== "Without Heat"
	![without heat](https://imgur.com/qtdX3QI.png)
=== "With Heat"
	![with heat](https://imgur.com/vo9CLUM.png)


You can also change the fire color. For this tutorial, I will use purple color and the secondary color pink. And the final result is this:

![FireBall](https://imgur.com/46PQFmf.png)

## Setting Objects
Place the **Fire_Ball** in **ServerStorage**. Add a **Script** in **ServerScriptService**, a **Local Script** in **StarterPlayerScripts**, and a **Remote Event** in **ReplicatedStorage**. Change the name of the remote event to **Shooter**. Our explorer hierarchy now looks like this:

![explorer](https://imgur.com/0QyDkoN.png)


## Scripting Client Side
In the local script, we will use [UserInputService](https://www.helpers-documents.ml/Tutorials/Scripting/Detecting_Keyboard_Inputs/).
Connect a function to `InputBegan`. In the function, check the input type. Get the mouse position and fire it along with the remote event to the server.

```lua
local UIS = game:GetService("UserInputService")
local Shooter_Event = game.ReplicatedStorage.Shooter
local Mouse = game.Players.LocalPlayer:GetMouse()

local Clock = 0
local CoolDown = 1 -- cooldown length

UIS.InputBegan:Connect(function(Input, GameProcessed)
	if Input.UserInputType == Enum.UserInputType.MouseButton1 and not GameProcessed then
		if os.clock() > Clock then

			Clock = os.clock() + CoolDown
			local Mouse_Pos = Mouse.Hit.Position -- getting the position where the mouse is pointing in the 3D world.
			Shooter_Event:FireServer(Mouse_Pos) -- firing the remote to the server with the mouse position.

		end
	end
end)
```

!!! info "CoolDown"
	Cooldowns are used to prevent some tasks like damaging from happening too quickly, so they're like cooldowns. Although this method isn't the conventional task.wait() one, it is far more superior and stable. **os.clock** is based on CPU time, so it provides more stability and accuracy than task.wait(), but it is used for comparing time instead of yielding.

## Scripting Server Side
On the server, we will connect a function to the remote event. In the function, we will perform the following steps

* Cloning Fireball, setting its position to the position of the player's character.
* Setting Attachment.
* Setting Velocity constraint.
* Setting velocity vector.

```lua
local Shooter_Event = game.ReplicatedStorage.Shooter
local Sample_Fireball = game.ServerStorage.FireBall

Shooter_Event.OnServerEvent:Connect(function(Player, Mouse_Pos)

    local Character = Player.Character

    local Fireball = Sample_Fireball:Clone()
    Fireball.CanCollide = false
    Fireball.Position = Player.Character.HumanoidRootPart.Position

    -- creating attachment
    local Attachment = Instance.new("Attachment")
    Attachment.Parent = Fireball

    -- creating velocity constraint
    local Velocity = Instance.new("LinearVelocity")
    Velocity.Attachment0 = Attachment

    -- setting the direction of velocity
    local Speed = 50 -- the speed of fireball/length of the vector
    Velocity.MaxForce = 9e6 -- setting maxforce to 9*10^6
    local Directional_Vector = (Mouse_Pos - Fireball.Position).Unit * Speed
    Velocity.VectorVelocity = Directional_Vector -- setting velocity

    Velocity.Parent = Fireball
    Fireball.Parent = workspace
    game.Debris:AddItem(Fireball, 3) -- destroying fireball after 3 seconds
end)
```

Now, you can test it.

![test](https://imgur.com/dgw1giK.png)

## Dealing Damage
For dealing damage, we will use the `Touched` event. As the fireball touches any object, we will check its parent and search for a humanoid. If it succeeds in finding the humanoid, then we are good to deal damage.

```lua
local Shooter_Event = game.ReplicatedStorage.Shooter
local Sample_Fireball = game.ServerStorage.FireBall

Shooter_Event.OnServerEvent:Connect(function(Player, Mouse_Pos)

    local Character = Player.Character

    local Fireball = Sample_Fireball:Clone()
    Fireball.CanCollide = false
    Fireball.Position = Player.Character.HumanoidRootPart.Position

    -- creating attachment
    local Attachment = Instance.new("Attachment")
    Attachment.Parent = Fireball

    -- creating velocity constraint
    local Velocity = Instance.new("LinearVelocity")
    Velocity.Attachment0 = Attachment

    -- setting the direction of velocity
    local Speed = 50 -- the speed of fireball/length of the vector
    Velocity.MaxForce = 9e6 -- setting maxforce to 9*10^6
    local Directional_Vector = (Mouse_Pos - Fireball.Position).Unit * Speed
    Velocity.VectorVelocity = Directional_Vector

    Velocity.Parent = Fireball
    Fireball.Parent = workspace
    game.Debris:AddItem(Fireball,3)

    Fireball.Touched:Connect(function(hit)
        if hit.Parent ~= Character and hit.Parent:FindFirstChild("Humanoid") then
            hit.Parent.Humanoid.Health -= 15
            Fireball:Destroy()
        end
    end)

end)
```

## Exploit Preventation

Everything we have done yet looks completely fine, but there is still an issue! An exploiter can easily bypass cooldown and spam the remote event. To avoid this, we need a server-side validation of requests. 

We will create a table that will carry record the cooldown of every player. The table will have player names as index/key and duration as the value. We will add the player's name on `PlayerAdded` and remove on `PlayerRemoving` events of `Players` service

```lua
local Shooter_Event = game.ReplicatedStorage.Shooter
local Sample_Fireball = game.ServerStorage.FireBall

local Players_Cooldown = {}
local CoolDown = 1 -- duration of cooldown

-- adding player's name to the table
game.Players.PlayerAdded:Connect(function(Player)
    Players_Cooldown[Player.Name] = 0
end)

-- removing player's name from the table
game.Players.PlayerRemoving:Connect(function(Player)
    Players_Cooldown[Player.Name] = nil
end)

Shooter_Event.OnServerEvent:Connect(function(Player, Mouse_Pos)

    if os.clock() > Players_Cooldown[Player.Name] then

        Players_Cooldown[Player.Name] = os.clock() + CoolDown

        local Character = Player.Character

        local Fireball = Sample_Fireball:Clone()
        Fireball.CanCollide = false
        Fireball.Position = Player.Character.HumanoidRootPart.Position

        -- creating attachment
        local Attachment = Instance.new("Attachment")
        Attachment.Parent = Fireball

        -- creating velocity constraint
        local Velocity = Instance.new("LinearVelocity")
        Velocity.Attachment0 = Attachment

        -- setting the direction of velocity
        local Speed = 50 -- the speed of fireball/length of  the vector
        Velocity.MaxForce = 9e6 -- setting maxforce to 9*10^6
        local Directional_Vector = (Mouse_Pos - Fireball.Position).Unit * Speed
        Velocity.VectorVelocity = Directional_Vector

        Velocity.Parent = Fireball
        Fireball.Parent = workspace
        game.Debris:AddItem(Fireball,3)

        -- dealing damage
        Fireball.Touched:Connect(function(hit)

            if hit.Parent ~= Character and hit.Parent:FindFirstChild("Humanoid") then

                hit.Parent.Humanoid.Health -= 15
                Fireball:Destroy()

            end
        end)
    end
end)
```

Now you can remove the cooldown from the client side if you don't want it.

## Closing
That's all for now! Hope you enjoyed this tutorial and can use it in your game. Again as I mentioned earlier, do not just copy the whole tutorial. It was designed to giving you some concepts and ideas on how you can make a fireball system. It's your job to utilize these concepts. Thanks for reading!
