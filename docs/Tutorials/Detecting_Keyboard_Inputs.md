# Detecting Keyboard Inputs With UserInputService
In this tutorial, I will be showing you how to detect keyboard inputs with [**UserInputService**](https://developer.roblox.com/en-us/api-reference/class/UserInputService). 

If you don't have a basic understanding of Lua and Roblox scripting I would recommend starting [**here**](https://rodevs-helpers.github.io/Helpers-Documents/Lua-Learning/basic-loops/) before going through this tutorial. Otherwise, you may get confused when we get into Events and other things.

## What is UserInputService?
UserInputService is a neat [**API Service**](https://developer.roblox.com/en-us/api-reference/index) that Roblox has put together to help up manage a client's user input, hence the name. A popular alternative to UserInputService is [**ContextActionService**](https://developer.roblox.com/en-us/api-reference/class/ContextActionService) which is sometimes preferred when you are working with input for different devices (mobile/console).

## Getting Started
First, we are going to need our **LocalScript**, for this tutorial, I will be putting it under **StarterPlayerScripts** and will be calling it **Sprint**. However, you can put this anywhere in a valid location for a LocalScript:

![](https://i.gyazo.com/e99e00cfd80aa4dd30ee5d1fe09a6213.png)


**Valid LocalScript Locations:**
* A Players Backpack, such as a child of a Tool
* A Players character model
* A Players PlayerGui
* A Players PlayerScripts.
* The ReplicatedFirst service

## The Fun Part
Now that we have our LocalScript, we can start getting into it.

First we are going to need to create a reference to **UserInputService:**
```lua
local UserInputService = game:GetService('UserInputService')
``` 
You can learn more about GetService [here](https://developer.roblox.com/en-us/api-reference/function/ServiceProvider/GetService)

Now that we have a reference to **UserInputService** we can start using it's functions and events. We will be using [InputBegan](https://developer.roblox.com/en-us/api-reference/event/GuiObject/InputBegan) and [InputEnded](https://developer.roblox.com/en-us/api-reference/event/GuiObject/InputEnded)

Before we make our events, I am going to define our sprint key as a constant. Using the global [Enums](https://developer.roblox.com/en-us/api-reference/datatype/Enum) that Roblox has made for us.  I will also be defining our [**LocalPlayer**](https://developer.roblox.com/en-us/api-reference/property/Players/LocalPlayer) which we can use to get our [**Character**](https://developer.roblox.com/en-us/api-reference/property/Player/Character).

You can find a complete list of **KeyCodes** [**here**](https://developer.roblox.com/en-us/api-reference/enum/KeyCode)

```lua
local UserInputService = game:GetService('UserInputService')
local SPRINT_KEY = Enum.KeyCode.LeftShift

local Player = game.Players.LocalPlayer
```

Now that we have our sprint key defined we can make our events:
```lua
local UserInputService = game:GetService('UserInputService')
local SPRINT_KEY = Enum.KeyCode.LeftShift

UserInputService.InputBegan:Connect(function(InputObject, GameProcessed)

end)

UserInputService.InputEnded:Connect(function(InputObject)

end)
```

As you can see, **InputBegan** and **InputEnded** both have a parameter: *InputObject* this is the object that contains all the information for the input that fired the event. This is how we can determine what key was pressed.

In the **InputBegan** event, you can see a second parameter called *GameProcessed*, this is a *boolean* value that will be true if the input that fired the event is being used by Roblox, this can be used to avoid doing something if a player is typing something in the Roblox chat. But for our tutorial, I will be ignoring that parameter because I want people to be able to sprint if they press the Shift Key, which can also be used for *ShiftLock*.

Now that we have our events, we need to make sure the key being pressed is our sprint key:
```lua
if (InputObject.KeyCode == SPRINT_KEY) then
```

Then inside that **if statement**, we can get our [**Character**](https://developer.roblox.com/en-us/api-reference/property/Player/Character) and [**Humanoid**](https://developer.roblox.com/en-us/api-reference/class/Humanoid):
```lua
		local Character = Player.Character or Player.CharacterAdded:Wait()
		local Humanoid = Character:WaitForChild('Humanoid')
```

Once we have the [**Humanoid**](https://developer.roblox.com/en-us/api-reference/class/Humanoid) we can set the [**WalkSpeed**](https://developer.roblox.com/en-us/api-reference/property/Humanoid/WalkSpeed) property to make the character sprint:

```lua
local UserInputService = game:GetService('UserInputService')
local SPRINT_KEY = Enum.KeyCode.LeftShift

UserInputService.InputBegan:Connect(function(InputObject, GameProcessed)
	if (InputObject.KeyCode == SPRINT_KEY) then
		local Character = Player.Character or Player.CharacterAdded:Wait()
		local Humanoid = Character:WaitForChild('Humanoid')
		
		Humanoid.WalkSpeed = 25
	end
end)

UserInputService.InputEnded:Connect(function(InputObject)

end)
```

Then finally, if we add that same code to our [**InputEnded**](https://developer.roblox.com/en-us/api-reference/event/GuiObject/InputEnded) event, and reverse the [**WalkSpeed**](https://developer.roblox.com/en-us/api-reference/property/Humanoid/WalkSpeed):
```lua
local UserInputService = game:GetService('UserInputService')
local SPRINT_KEY = Enum.KeyCode.LeftShift

UserInputService.InputBegan:Connect(function(InputObject, GameProcessed)
	if (InputObject.KeyCode == SPRINT_KEY) then
		local Character = Player.Character or Player.CharacterAdded:Wait()
		local Humanoid = Character:WaitForChild('Humanoid')
		
		Humanoid.WalkSpeed = 25
	end
end)

UserInputService.InputEnded:Connect(function(InputObject)
	if (InputObject.KeyCode == SPRINT_KEY) then
		local Character = Player.Character or Player.CharacterAdded:Wait()
		local Humanoid = Character:WaitForChild('Humanoid')
		
		Humanoid.WalkSpeed = 16
	end
end)
```


## Done
Hey Presto! If you followed this tutorial correctly, your character should speed up while you are holding the *SPRINT_KEY* and go back to normal when you release the key.

I hope you enjoyed learning about [**UserInputService**](https://developer.roblox.com/en-us/api-reference/class/UserInputService).  

* [Learning Resources](https://developer.roblox.com/en-us/)
