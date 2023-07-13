!!! attention "Note"
    Before reading this tutorial, you should know about [metatables](https://docs.rodevs.com/Scripting/Advanced-Courses/metatables/). An explanation of metatable exists in the Lua-Learning folder.

# What are Proxy Tables?
Proxy table are Tables that allow you to detect when a table is updated or changed using __newindex

## How to set on up
What we want to do it use __newindex to reference the Real Data inside of the Proxy Table. 

We can set it up like this:

```lua
local Proxy = {}

Proxy.__newindex = function(self,key,value)
    self.RealData[key] = value -- without this the key would need be set to the new value
    print("Detected Change at",key,"new Value",value)
end


function Proxy.new(DataTable)
    return setmetatable({RealData = DataTable or {}},Proxy)
end

return Proxy
```

This is basically all you need for a proxy table to function 

```lua
local Proxy = require(Path.To.Proxy.Module)
local data ={
    A = 1,
    Hao = 2
}
local ProxyTable = Proxy.new(data)

ProxyTable.A = 2 --> Detected Change at A new Value 2
ProxyTable.B = 3 --> Detected Change at B new Value 3 
ProxyTable.Hao = nil --> Detected Change at Hao new Value nil
```

## Features you can add to your proxy table
You can also add more features to the proxy table so that the proxy table can act like a normal table. here are some examples:

adding the __index metamethod
```lua
-- this will allow you to do ProxyTable["A"] normally to get the data
Proxy.__index = function(self,key)
    return self.RealData[key]
end

--Example Use Case
print(ProxyTable.ProxyTable.A) -- > 2
print(ProxyTable.A) -- > 2
```

adding the __iter metamethod
```lua
-- this will allow the proxy table to be iterated by a for loop 
Proxy.__iter = function(self)
    return next,self.RealData -- similar to pairs(table)
end

--Example Use Case
for i,v in ProxyTable do
    print(i,v) --> A 2 | B 3     
end
```
adding a bindable event to use as a changed event
```lua
-- this will allow the proxy table to be iterated by a for loop 
Proxy.__newindex = function(self,key,value)
    self.RealData[key] = value
    self.Changed:Fire(key,value)
end

function Proxy.new(DataTable)
    return setmetatable({RealData = DataTable or {},Changed = Instance.new("BindableEvent")},Proxy)
end

--Example Use Case
ProxyTable.Changed.event:Connect(function(key,value)
    print("table was modified")
end)
```
Check out this [**link**](https://create.roblox.com/docs/scripting/luau/metatables) for more metamethods

# Conclusion 
If you think you're going to use RealData as a key name you can name the key to something random so that when you do ProxyTable.RealData={} it wouldn't override your real data with an empty table. Anyways thats it for this tutorial, hope this helps 