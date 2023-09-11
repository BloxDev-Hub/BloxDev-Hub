---
title: What Are Attributes?
template: docs.html
comments: true
hide:
  - navigation
---

# Attributes
In Roblox Attributes of an instance are just like it's properties but custom properties.
It means you can create them, remove them, edit them. They are pretty useful and they also save you from having multiple value instance like ``string value``, ``bool value``, ``int value``.
You can create them manually or by using a script. In this guide we will be creating them via ``scripts``.

# Creating Attributes!
## SetAttribute()
In order to create an attribute we use a method **SetAttribute()**. This method takes two arguments:

1. Name Of the attribute
2. Value

```lua
local Part = workspace.Part --referencing a part in the workspace
--Creaing attribute of part
Part:SetAttribute("Nickname","eden")
```

In the above code we created an attribute of part and named that attribute `Nickname` and set its value to a string "eden".
Now if you run the script then you can find this attribute in the **Properties** window. But now how can we use this attribute?.

# Getting Attributes!
## GetAttribute()
When ever we want to get value of an attribute of any instance, we call a method **GetAtribute()** over the instance. This method takes only 1 argument:

1. Name of the attribute.

```lua
local Part = workspace.Part
--creating an attribute of part
Part:SetAttribute("Nickname","eden")
--getting value of the attribute "Nickname".
local Nickname = Part:GetAttribute("Nickname")
print(Nickname)
```
Output:

```
eden
```

**Note:** You can't get value of any attribute by ``Part.NameOfAttribute``. Name of the attribute must be *String*.

# Getting all attributes!
## GetAttributes()
In order to get all attributes of an instance you need to call **GetAttributes()** (*GetAtrributes() and GetAtrribute() two different methods*) over the instance. This method returns a dictionary of names and the values of all attributes of the instance.

Sample Code:

```lua
local Part = workspace.Part
--creating an attribute of part
Part:SetAttribute("Nickname","eden")
Part:SetAttribute("IsAlive",true)
--getting value of all the attributes.
for Name , Value in pairs(Part:GetAttributes()) do
   print(Name,Value)
end
```

Output:

```
Nickname eden
IsAlive  true
```


# Editing/Removing attributes!
Now if we want to change nickname of the part to "heaven". We will again use **SetAttribute()**. If the attribute with the given name already exist it just change it's value but if the attribute with this name doesn't exist, it creates the attribute then set its value.

Here is an example code:

```lua
local Part = workspace.Part
--creating an attribute of part
Part:SetAttribute("Nickname","eden")
local Nickname = Part:GetAttribute()
print(Nickname)
Part:SetAttribute("Nickname","Heaven")
Nickname = Part:GetAttribute("Nickname")
print(Nickname)
```

Output:

```
eden
Heaven
```

If we want to remove any attributes we will just set it's value to ``nil``.

```lua
Part:SetAttribute("IsAlive", nil)
```
Boom! its gone now.

# Detecting Changes!
## GetAttributeChangedSignal()
If we want to detect change of any specific attribute we use ``GetAttributeChangedSignal()``.
## AttributeChanged
If we want to detect change of any attribute we use ``AttributeChanged``
Here is an example for you!

```lua
Part:GetAttributeChangedSignal("Nickname"):Connect(function()
     print("nickname changed")
end)

Part.AttributeChanged:Connect(function(nameoftheattrubute)
     print(nameoftheattribute .."Changed")
end)
```

# Thanks For Reading

In case of any mistake feel free to report this article and don't forget to leave your reviews!
