---
title: Understanding events
template: docs.html
comments: true
hide:
  - navigation
---

# Events on Roblox Studio

Events are one of the most used objects in Roblox Studio, when scripting on the platform you will make encounters with them very frequently and I could say that you will use them more than once in your game, there is a problem with beginners not fully comprehending this so-called "events" and sometimes, they end up misusing them, that's why I decided to make this article.

We are going to learn what exactly is an event, how to use it, how to NOT use it, and some good practices when using it.

## What is an event?

An event, formally called an [RBXScriptSignal](https://developer.roblox.com/en-us/api-reference/datatype/RBXScriptSignal) or [RobloxScriptSignal](https://developer.roblox.com/en-us/api-reference/datatype/RBXScriptSignal) it's a Roblox object that calls user-made functions when a certain in-game event happens, you can use them to know whenever a part touches another, when the user began an input, when a frame gets rendered, and more! That's why events are used very frequently and you can't just ignore them, they are the main way of knowing when something happened and assigning code for when it does happen, you will need to use them sooner or later.

Each instance type counts with their own events, for example, BaseParts have [Touched](https://developer.roblox.com/en-us/api-reference/event/BasePart/Touched) and [TouchEnded](https://developer.roblox.com/en-us/api-reference/event/BasePart/TouchEnded), services count with events too, Players service has the [PlayerAdded](https://developer.roblox.com/en-us/api-reference/event/Players/PlayerAdded) and [PlayerRemoving](https://developer.roblox.com/en-us/api-reference/event/Players/PlayerRemoving) events, you can also create your own events with [BindableEvents](https://developer.roblox.com/en-us/api-reference/class/BindableEvent) or make them from scratch in a script (after you understand how they work of course)

## Usage of an event

Events have two methods which are the only way to use them, those methods are **Connect** and **Wait**.

Connect method requires only one parameter which is the function to connect to the event, this will add the function to the listeners of the event, and it will be called when the event fires, the method also returns a so-called [RBXScriptConnection](https://developer.roblox.com/en-us/api-reference/datatype/RBXScriptConnection) or Connection which we are going to talk about later.

```lua
RBXScriptSignal:Connect(function()
    print("Event fired!")
end)
```

??? info "Clarification when using Connect"
    In this example script, we created an anonymous function inside the parenthesis and the function can't be accessed from any other part of the script, that's why you see a parenthesis after the end, to close the Connect method call, but if the function is going to be used multiple times independent of the event or just for the sake of readability you could assign the function to a variable and just pass it as an argument to the Connect method:

    ```lua
    local function Listener()
        print("Event fired!")
    end

    RBXScriptSignal:Connect(Listener)
    ```

The Wait method yields the current thread when called, and it will resume it until the event gets fired, and if you didn't understand that, don't worry, you will in the future, but in basic words, it will pause the script and will wait until the event gets fired to resume it, this unlike the Connect method will only listen for the next time the event fires after calling the method, after that it will not listen to the event.

```lua
print("Waiting for event to fire!")
RBXScriptSignal:Wait()
print("Event fired!")
```

??? warning "Information about Wait method"
    You need to be very cautious when using the Wait method over events, if for some reason your event never fires let's say, because of the instance getting destroyed, your script will never resume.

## How an event works

The way of how an event works it's very simple, it's just based on storing values, for visualizing it we can say that when calling the method Connect, the event will store the function passed as an argument to a listeners table returning the connection made, and when calling the Wait method it will pause the thread and will store it on another table.

<div class="mermaid">
graph LR
    a[Call] --- b[Connect]
    b --- c[Store function in table]
    c --- d[Return connection]
    a --- e[Wait]
    e --- f[Yield thread]
    f --- g[Store thread in table]
</div>

After that, when the event gets fired it will only need to look for every function in the listeners table and call it, the same with threads, look for every thread in the table and resume it returning what the event does return.

<div class="mermaid">
graph LR
    a[Fire] --- b[Listeners]
    b --- c[Call every function]
    a --- d[Threads]
    d --- e[Resume every thread]
    e --- f[Return values]
</div>

This of course accounts for Filtering Enabled.

Events as mentioned earlier can return or pass values depending on the situation, for example, the BasePart's [Touched](https://developer.roblox.com/en-us/api-reference/event/BasePart/Touched) event passes the other part that touched our part as an argument to the connected functions, and returns it to the Wait call, knowing this we can do:

```lua
BasePart.Touched:Connect(function(otherPart)
    print(otherPart.Name.." touched our BasePart")
end)
```

```lua
local otherPart = BasePart.Touched:Wait()
print(otherPart.Name.." touched our BasePart")
```

For knowing what does an event returns we recommend you check Roblox's API reference.

## Events are not if statements!

The most common error that beginners do when using events is using them as if they were if statements nesting them like this:

```lua
event1:Connect(function()
    event2:Connect(function()
        ...
    end)
end)
```

Or even using them like this:

```lua
while true do
    wait()
    event:Connect(function()
        ...
    end)
end
```

This is completely wrong, and it's considered a misuse of events! Why? Well it's simple, the ones who wrote the code above may be misunderstanding what events are used for and they are using them to check if something happened and, as we said, their purpose is not that.

For the first problem we can say, as we saw, when calling the Connect method the event will create a connection and return it to us, this means that every time the first event fires, a new connection for the second event will get create, this will lead to the code running many times, so if for example the first event ran five times, when the second event fires, the function will get called ten times! And not also that, if we are using anonymous functions (like in our case) we are going to be creating a new function every time and also as we have no reference for the connection of the second event we have no way of this to stop!

A simple solution for this, would be using actual if statements and not nesting the events, for example:

```lua
local checkVariable = false

event1:Connect(function() checkVariable = true end)
event2:Connect(function()
    if checkVariable then
        ...
    end
end)
```

This will depend on every case, but in general, this is what most people try to do.

## Disconnecting our connections

As we said earlier, Connect method returns a RBXScriptConnection or Connection, this datatype or object contains one but powerful method, which is **Disconnect** and as you guessed, when it gets called it disconnects the listener function from the event, the exact opposite thing that Connect does. You may be asking "Why would be this useful?" well, let me explain to you creating another solution for the first problem above.
```lua
local connection -- Initializes the variable on nil

event1:Connect(function()
    if not connection then -- If connection it's nil
        connection = event2:Connect(function() -- We set our connection
            ...
            connection:Disconnect() -- We disconnect our connection
        end
    end
end)
```

This may not be the best solution but for the sake of explaining to you what disconnect does, I think it's pretty good, disconnecting a connection when the event it's not going to be used again or similar it's a good practice, since it can avoid us to memory leaks and other weird stuff that could happen in the background; this of course it's not necessary all the times because for example, when an instance gets destroyed, all the connections do too.

## Memory leaks

As we mentioned above, not disconnecting events in some cases can lead to more memory usage, or memory leaks, lets take as example the second problem mentioned above; every 1/30 seconds we are creating a new connection for the event, this is not good because we are using more memory for storing those connections and all of that stuff, now if you run some code like that, eventually you will see that, when time passes your game can increase its activity, or even experience lag spikes or poor performance, so if your game it's experiencing some of those problems you may want to look over your events and handle them better

## Thanks for reading

Thanks for reading the article and I hope you understood how to use events, how they work and some good practices.