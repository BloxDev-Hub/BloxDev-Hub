---
title: Bindable Events and Functions
template: docs.html
comments: true
hide:
  - navigation
---


# Bindables
Bindable events and functions are pretty much similar to [Remote Events and Functions](https://rodevs-helpers.github.io/Helpers-Documents/Luau-Learning/Remote_Events_And_Functions/). However, In this guide, we will explain bindable events and functions from scratch. 

## Basic Info
Bindable events or functions are used for communication between server-side [Script(s)](https://developer.roblox.com/en-us/api-reference/class/Script).
Bindable events offer one-way communication. However bindable functions are capable of performing two-way communication. This doesn't mean that bindable functions are anyway better than bindable events. They should be according to their use cases. 

## Bindable Events
Using bindable events, an event can be fired from one script and can be received on another script.

### How to use bindable events?
First of all, add a bindable event in [ServerStorage](https://developer.roblox.com/en-us/api-reference/class/ServerStorage)

![adding](https://imgur.com/tT1XxVw.png)

By default its name is "Event" but I have changed its name to "BindableEvent" just to make it easier to understand.

Now we will add two [Script(s)](https://developer.roblox.com/en-us/api-reference/class/Script) in [ServerScriptService](https://developer.roblox.com/en-us/api-reference/class/ServerScriptService). Name one of them "Sender" and the other "Receiver". 

![Scripts](https://imgur.com/JZJLhRn.png)

We will use "Sender" for firing the event and "Receiver" for receiving that event. For firing a bindable event, we will use a method **[BindableEvent:Fire()](https://developer.roblox.com/en-us/api-reference/function/BindableEvent/Fire)**. **[BindableEvent.Event](https://developer.roblox.com/en-us/api-reference/event/BindableEvent/Event)** will be used for receiving events. Let's implement this!

Code on "Sender":

```lua
game.ServerStorage.BindableEvent:Fire("eden is cool")
```
!!! note ""
	Any number of arguments can be passed when firing an event.

Code on "Receiver":

```lua
game.ServerStorage.BindableEvent.Event:Connect(function(value)
	print(value) --eden is cool
	print("event recieved")
end)
```
Yep, it's that easy and simple. Now when you run the game and as the event is received. You can see "event received" in the output window.

![output1](https://imgur.com/N7X2Vom.png)

## Bindable Functions
For bindable functions, we will use the same setup for script and place the bindable function in [ServerStorage()](https://developer.roblox.com/en-us/api-reference/class/ServerStorage). The explorer tree will look like,

![explorer](https://imgur.com/9iSqV6D.png)

As done earlier, we will use "Sender" for invoking the bindable function and "Receiver" for binding a function to the bindable function. For doing so, we will be using **[BindableFunction:Invoke](https://developer.roblox.com/en-us/api-reference/function/BindableFunction/Invoke)** and **[BindableFunction.OnInvoke](https://developer.roblox.com/en-us/api-reference/callback/BindableFunction/OnInvoke).**

Code on "Sender":

```lua
game.ServerStorage.BindableFunction:Invoke("eden is cool")
```

Code on "Receiver":

```lua
game.ServerStorage.BindableFunction.OnInvoke = function(value)
	print(value) --eden is cool
	print("function invoked")
	return true
end
```

![Output2](https://imgur.com/rOGpJH1.png)

### Drawbacks
!!! warn ""
    * Once invoked the bindable function, the thread will yield until any callback is found.
    * If the callback isn't set, the thread will yield forever.
    * In bindable events, you can create multiple connections on the event but you can not bind multiple functions to [BindableFunction:Invoke](https://developer.roblox.com/en-us/api-reference/function/BindableFunction/Invoke)

# Closing!
I hope, you enjoyed read it! If you find any typos, or any sort of flaws then please report it [here](https://rodevs-helpers.github.io/Helpers-Documents/Others/Help_Us%21/).