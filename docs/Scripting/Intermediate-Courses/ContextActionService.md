---
title: Binding Actions!
template: docs.html
comments: true
hide:
  - navigation
---

# Context Action Service
Context action is a service that helps in binding actions to inputs. It is similar to [UserInputService](https://developer.roblox.com/en-us/api-reference/class/UserInputService) but has some cooler features.

## Understanding Use Case
Context action service works according to its name. It enables you to bind and unbind actions on input based on conditions. Its use case can be easily understood by the following examples.

* A player may open a door only when he is closer to it.
* A player may interact with an NPC only when they are inside the shop.

Using context action service, you will bind an action when the player is closer to the door. As the player moves away from the door, you should unbind the action.

## Viewing Bound Actions
In order to view the bound actions, open the console (either using the main menu or the `F9` key). Visit the "**Action Bindings**" tab. It will display all the bound actions. These also include actions bound by Roblox core scripts. 

## Action Priorities
Via context action service, you can bind multiple actions to an input. However, those actions will be performed based on different priorities. The most recent bound action will have the highest priority. These priorities can be changed using [BindActionPeriority](https://developer.roblox.com/en-us/api-reference/function/ContextActionService/BindActionAtPriority).

## Multiple Medium Input Detection
ContextActionService also supports gamepads, and touch screens. Using contextactionservice, you can create on-screen touch buttons. These buttons are rendered as long as the action is bound. These buttons can be customized by changing their positions, and labels.

# Usage
In this guide, we will cover some basic fundamental functions of ContextActionService.

## Binding Actions
For binding an action we use the method `:BindAction()`. This function takes four arguments

* Name of Action   | type: [String](https://developer.roblox.com/en-us/articles/String)
* Function handling the action   | type: [Function](https://developer.roblox.com/en-us/articles/Function)
* Condition for creating touch button   | type: [Bool](https://developer.roblox.com/en-us/articles/Boolean)
* InputObject   | [KeyCode](https://developer.roblox.com/en-us/api-reference/enum/KeyCode) or [UserInputType](https://developer.roblox.com/en-us/api-reference/enum/UserInputType)

### Name Of Action
The name of action can be any suitable string that represents the action.

### Function Handling The Action
This function will be called whenever the input key (to which action is bound) is pressed. This function is called with the following parameters

* Name of action that was originally given when binding action.   | type: [String](https://developer.roblox.com/en-us/articles/String)
* State of the input (These include Begin, Change, End, or Cancel).   | type: [UserInputState](https://developer.roblox.com/en-us/api-reference/enum/UserInputState)
* An object containing information about the input.   | type: [InputObject](https://developer.roblox.com/en-us/api-reference/class/InputObject)

Example function:

```lua
local function Action_Handler(ActionName, InputState, InputObject)
    if InputState == Enum.UserInputState.Begin then
        print("Teerach is an English geek")
    else
        print("Paper was made of China!")
    end
end
```

### Mobile Button
The third argument of `BindAction()` is a bool value. To enable the mobile button, this argument should be `true` or otherwise `false`.

### Input type
Basically the [Enums](https://developer.roblox.com/en-us/api-reference/datatype/Enums) of key codes or user input types.

```lua
local ContextActionService = game:GetService("ContextActionService")

local function Action_Handler(ActionName, InputState, InputObject)
    if InputState == Enum.UserInputState.Begin then
        print("EdenRose is blessing the world with her present")
    else 
        print("Thanks to helper department for such an impressive documentation")
    end
end

ContextActionService:BindAction("Input Detection", Action_Handler, true, Enum.KeyCode.P)
```

Now, we have bound the action **Input Detection** with the key "P"

## Unbinding Actions
Once bound, you can unbind an action when you are done with it. This can be done using `:UnbindAction()`. This method takes the name of the bound action.

```lua
ContextActionService:UnbindAction("Input Detection")
```

# Closing!
That's pretty much all of it. I hope you enjoyed reading it and now have a basic understanding of ContextActionService. In case of any mistakes, typos, etc. Please report the article. You can also give us reviews [here](https://rodevs-helpers.github.io/Helpers-Documents/Others/Help_Us%21/)