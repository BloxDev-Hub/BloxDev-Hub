---
title: Making Simple Gun
---

# Introduction
In this tutorial, we will be making a simple, blocky gun. This tutorial requires a basic knowledge of the following topics

* [Tools](https://www.helpers-documents.ml/Luau-Learning/Tool/)
* [Vectors](https://www.helpers-documents.ml/Luau-Learning/Vector3/)
* [Client And Server Communication](https://www.helpers-documents.ml/Luau-Learning/Remote_Events_And_Functions/)

It's highly recommended not to proceed if you haven't covered those topics.

## Making a tool
First of all, we will make a tool that will be our gun. Because this tutorial will only cover the fundamentals of a weapon, we will not emphasize the shape of the gun.

Add a part in **Workspace** and name it **Handle**.

![gunblock](
https://imgur.com/R0y5POC.png)

Scale the part according to the hand of the player's character.

![partrender](
https://imgur.com/BGMFGVT.png)

Now add a **Tool** in **workspace** and parent the **Handle** to the tool. Our explorer hierarchy now looks like this:

![explorertool](
https://imgur.com/6BbUi9p.png)

If you want to test, place your tool in **StarterPack**.

![starterpack](
https://imgur.com/OZ6h3et.png)

Click the play button (or press F5). 

![play1](
https://imgur.com/3YFnKvy.png)

## Setting Up
Now we will set up everything we need for our weapon to work.

Add a [Local Script]() in the tool.
Add a **Remote Event** in the [Replicated Storage]().
Add a **Script** in [ServerScriptService]().

![steupexplorer](
https://imgur.com/VusMpxQ.png)

## Client Side
On the client side (local script) we will check when the tool is used and request the server to shoot a bullet. First of all, we will store everything we need in variables to make the code look cleaner.

```lua
local gun = script.Parent -- our tool
local remote_event = game.ReplicatedStorage.RemoteEvent
local mouse = game.Players.LocalPlayer:GetMouse() -- getting the mouse of player
```

We will create a function `shooter`. This function will be responsible for making requests when the tool is used. It will be done by firing the remote event on the server. This remote event will also carry the position where the player's mouse is pointing at.

```lua
local gun = script.Parent --our tool
local remote_event = game.ReplicatedStorage.RemoteEvent -- remote event
local mouse = game.Players.LocalPlayer:GetMouse() -- getting the mouse of player
local gun_connection -- variable for caching connection

local function shooter()
    local mouse_pos = mouse.Hit.Position -- the 3d world position where the mouse is pointing.
    local origin = gun.Handle.Position
    remote_event:FireServer(mouse_pos, origin)
end
```

Now we will connect a function to the `Equipped` event of the tool. In this function, we will connect the shooter function to the `Activated` event of the tool. This connection will be cached in a variable `gun_connection` so we can disconnect it as the tool is unequipped (the `Unequipped` event is fired).

```lua
local gun = script.Parent -- our tool
local remote_event = game.ReplicatedStorage.RemoteEvent -- remote event
local mouse = game.Players.LocalPlayer:GetMouse() -- getting the mouse of player
local gun_connection -- variable for caching connection

local function shooter()
    local mouse_pos = mouse.Hit.Position -- the 3d world position where the mouse is pointing.
    local origin = gun.Handle.Position -- the origin of bullet
    remote_event:FireServer(mouse_pos, origin)
end

gun.Equipped:Connect(function()
    gun_connection = gun.Activated:Connect(shooter)
end)

gun.Unequipped:Connect(function()
    gun_connection:Disconnect()
end)
```

Congrats! our client side is done. Every time tool is equipped the connection on the `Activated` event is established and `shooter` is called whenever the player clicks/activates the tool.

## Server Side
On the server side, we have the following things to do:

* Creating bullets.
* Setting up velocity constraint.
* Calculating directional vector 
* Dealing damage.
* Destroying bullet.

But firstly, we have to check when the remote event is fired.

```lua
game.ReplicatedStorage.RemoteEvent.OnServerEvent:Connect(function(player, mouse_pos)

end)
```

### Creating Bullets
You can create a bullet of any size, color, and shape you want.
I will be creating blocky shape neon yellow bullets.

```lua
game.ReplicatedStorage.RemoteEvent.OnServerEvent:Connect(function(player, mouse_pos)
    -- creating bullets
    local bullet = Instance.new("Part")
    bullet.Color = Color3.new(1, 1, 0.133333)
    bullet.Size = Vector3.new(1,1,1)

end)
```
### Setting Up Velocity Constraint
We will use **Linear Velocity** to apply a continuous velocity on bullets. For doing so, we have to create an attachment and parent it to the bullet. Then we will create a `LinearVelocity` constraint and assign the attachment to the `Attachment1` property of **LinearVelocity**. It will be parented to bullet as well.

```lua
game.ReplicatedStorage.RemoteEvent.OnServerEvent:Connect(function(player, mouse_pos)
  
	-- creating bullet
	local bullet = Instance.new("Part")
	bullet.Color = Color3.new(1, 1, 0.133333)
	bullet.Size = Vector3.new(1,1,1)
	bullet.CanCollide = false

	-- creating attachment
	local attachment = Instance.new("Attachment")
	attachment.Parent = bullet

	-- reating velocity constraint
	local velocity = Instance.new("LinearVelocity")
	velocity.Attachment0 = attachment
	velocity.Parent = bullet
end)
```

### Calculating Directional Vector
Linear velocity requires a `Vector3` value that specifies the direction of velocity. We need a vector that originates from the tool and points in the direction where the mouse of the player is pointing at.

```lua
game.ReplicatedStorage.RemoteEvent.OnServerEvent:Connect(function(player, mouse_pos, origin)
    -- creating bullet
    local bullet = Instance.new("Part")
    bullet.Color = Color3.new(1, 1, 0.133333)
    bullet.Size = Vector3.new(1,1,1)
    bullet.CanCollide = false

    -- creating attachment
    local attachment = Instance.new("Attachment")
    attachment.Parent = bullet

    -- creating velocity constraint
    local velocity = Instance.new("LinearVelocity")
    velocity.Attachment0 = attachment
    velocity.Parent = bullet

    -- setting the direction of velocity
    local speed = 50 -- speed of bullet/length of vector
    velocity.MaxForce = 9e6 --setting maxforce to 0 exponent 9
    local directional_vector = (mouse_pos - origin).Unit * speed
    velocity.VectorVelocity = directional_vector
    
end)
```

### Dealing Damage
This is another important part of gun mechanics. We will use the `Touched` event, as the bullet touches any object we will check its parent and search for a humanoid. If it succeeds in finding the humanoid then we are good to deal damage.

??? warning
        Always make sure that you are not damaging humanoid of shooter.

```lua
game.ReplicatedStorage.RemoteEvent.OnServerEvent:Connect(function(player, mouse_pos, origin)
	-- creating bullet
	local bullet = Instance.new("Part")
	bullet.Color = Color3.new(1, 1, 0.133333)
	bullet.Size = Vector3.new(1,1,1)
	bullet.CanCollide = false

	-- creating attachment
	local attachment = Instance.new("Attachment")
	attachment.Parent = bullet

	-- creating velocity constraint
	local velocity = Instance.new("LinearVelocity")
	velocity.Attachment0 = attachment
	velocity.Parent = bullet

	-- setting the direction of velocity
	local speed = 50 -- speed of bullet/length of vector
	velocity.MaxForce = 9e6 -- setting maxforce to 9 exponent 9
	local directional_vector = (mouse_pos - origin).Unit * speed
	velocity.VectorVelocity = directional_vector

	--deal damage
	bullet.Touched:Connect(function(hit)
		if hit.Parent ~= player.Character and hit.Parent:FindFirstChild("Humanoid") then
			hit.Parent.Humanoid.Health -= 15
			bullet:Destroy()
		end
	end)

	bullet.Parent = workspace
	bullet.Position = origin
end)
```

### Destroying Bullet
Lastly, we will destroy the bullet after a few seconds via debris service.

```lua
game.ReplicatedStorage.RemoteEvent.OnServerEvent:Connect(function(player, mouse_pos, origin)
	--creating bullet
	local bullet = Instance.new("Part")
	bullet.Color = Color3.new(1, 1, 0.133333)
	bullet.Size = Vector3.new(1,1,1)
	bullet.CanCollide = false

	--creating attachment
	local attachment = Instance.new("Attachment")
	attachment.Parent = bullet

	--creating velocity constraint
	local velocity = Instance.new("LinearVelocity")
	velocity.Attachment0 = attachment
	velocity.Parent = bullet

	--setting the direction of velocity
    	local speed = 50 -- speed of bullet/length of vector
    	velocity.MaxForce = 9e6 --setting maxforce to nine exponent 9
    	local directional_vector = (mouse_pos - origin).Unit * speed
    	velocity.VectorVelocity = directional_vector

    	--deal damage
    	bullet.Touched:Connect(function(hit)
        	if hit.Parent ~= player.Character and hit.Parent:FindFirstChild("Humanoid") then
            		hit.Parent.Humanoid.Health -= 15
            		bullet:Destroy()
        	end
   	end)
	
	bullet.Position = origin
    	bullet.Parent = workspace
    	
   	game.Debris:AddItem(bullet, 8)
end)
```
![final](
https://imgur.com/QrJCp0p.png)

## Closing
I hope this tutorial helped you and gave you an idea of how you can design your shooting weapons. You can customize it a lot by changing bullets, shooting styles, and stuff. Thanks a lot for reading! Byee!
