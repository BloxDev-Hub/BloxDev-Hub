---
Title: basics_of_properties
---

# Properties
Properties are a very key aspect in instances and Roblox programming. A property is an aspect of an **Instance** which can be changed.

## Using Properties
Properties are very important and can be used in multiple ways. Here's how to access property and edit a property. Here I'll be changing the properties of a part via script.

```lua
local Part = workspace.Part/Instance.new('Part') -- Example
Part.Name = 'Part' -- We use . to get a property
Part.Parent = workspace
Part.BrickColor = BrickColor.new('Really Red')
```

### Common Mistakes Made When Using Properties
Lots of new scripters commonly make the mistake of **Indirect Changes**.
An indirect change is where you change the value of a **Variable** but not the value of your property.

=== "Code"
    ```lua
    local Cash = Player.leaderstats.Cash.Value -- 25
    Cash = 50
    print(Cash)
    print(Player.leaderstats.Cash.Value) 
    ```
=== "Output"
    ```
    50
    25
    ```

The reason didn't work is because when we want to change something like this we have to access the value directly.

Correct way of doing this
=== "Code"
    ```lua
    local Cash = Player.leaderstats.Cash
    Cash.Value = 50
    print(Cash)
    print(Player.leaderstats.Cash.Value) 
    ```
=== "Output"
    ```
    50
    50
    ```

## How to use properties outside of scripts
Firstly, make sure you have the properties tab enabled. If you don't, click the view tab at the top of roblox studio and click on properties(near the left).

![viewtab](https://imgur.com/CicwqfX.png)

Once that is enabled you can change the properties of anything!
Click on the instance you want to change and look at the properties menu. Loads of things are waiting to be changed to your liking.

![property](https://imgur.com/xWPj57h.png)


### Changing basic properties
For this section, we'll be changing some common properties of a part.

![initial](https://imgur.com/EpRjzmV.png)

Firstly, we'll change the brickcolor and size properties. This can be easily done by 

```lua
local part = workspace.Part

--changing brickcolor
part.BrickColor = BrickColor.new("Really red")

--changing size
part.Size = Vector3.new(10,10,10)
```

![final](https://imgur.com/KIbjpuw.png)
Those are just some basic things you can change with properties!

## Common properties
Here are some common properties that every Instance should have.

```lua
.Name
.Parent
.Archivable 
.ClassName
```


## GetPropertyChangedSignal
GetPropertyChangedSignal is an event to detect whenever a property is changed.
I'll be demonstrating a part for this

```lua
local Part = Instance.new('Part')/workspace.Part

Part:GetPropertyChangedSignal('Name'):Connect(function()
    print(Part.Name) -- SalzuIsCool,EdenIsBest
end)

Part.Name = 'SalzuIsCool'
Part.Name = 'EdenIsBest'
```

## Closing
Thanks for reading my article. Please remember to report any errors found!