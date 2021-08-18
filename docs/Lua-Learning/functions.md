---
title: Functions
---

# Pre-requisites
You should have an understanding of variables first before proceeding.

# Functions
Suppose to say you need to spawn a part with a specific set of properties. For example, you might want the new part to have:
* `CanCollide` set to false (meaning anything can pass through it).
* `Anchored` set to true (so it stays rooted and doesn't get affected by physics).
* `Material` set to smooth plastic.
* `Color` set to lime green.
* `Transparency` set to 0.5.

Seems simple, right? It is! So let's write the code for it. 

```lua
-- Objectively the best way to spawn a part.
--    - valk
local part = Instance.new("Part")
part.CanCollide = false
part.Anchored = true
part.Material = Enum.Material.SmoothPlastic
part.Color = Color3.fromRGB(0, 0, 255)
part.Transparency = 0.5
part.Parent = workspace
```

Now what if we have to spawn the same part 100 times, and in different circumstances? Does this mean we have to copy the code above 100 times?

No, not necessarily.

## The Answer
Enter: functions! Functions contain sets of instructions that run whenever it's called. You first define a function, and then you run it. 

## Defining functions
To define a function is easy. Declare that it is a function using `function`, then give your function a name!

Taking our part spawning example, let's now write a function to keep all that code in one easy-to-find function! Let's name the function `SpawnPart` too.

```lua
local function SpawnPart() -- Remember to add brackets beside your function name! Otherwise, the game won't recognize that you're trying to define a function.
	local part = Instance.new("Part")
	part.CanCollide = false
	part.Anchored = true
	part.Material = Enum.Material.SmoothPlastic
	part.Color = Color3.fromRGB(0, 0, 255)
	part.Transparency = 0.5
	part.Parent = workspace
end
```

However, we are only done with the first part - defining a function. If you ran the code as is, you'll notice that nothing prints out. We'll have to run/call our function.

## Calling functions
Calling a function is even easier - just type the name of the function and add brackets beside it! `()`

```lua
SpawnPart() -- Be sure to leave brackets here! Otherwise, the game won't recognize that you're calling a function!
```

Now your workspace should have a part with all those properties.

## Parameters
Now, what if we want the part to have a transparency value that we can specify and change? Fret not, we can do that with functions too - by using parameters.

Remember the bracket that we left beside the name when we first defined the function?

```lua
local function SpawnPart() -- This.
end
```

We can actually place parameters inside them. Parameters allow us to input values/data into our function, allowing our function to do stuff with them.

```lua
local function SpawnPart(transparency)
end
```

When we write our defining code for our function, notice how we can write `transparency` as if it was a proper variable.

Let's now modify our code to work with the parameter we gave the function.

```lua
local function SpawnPart(transparency)
	local part = Instance.new("Part")
	part.CanCollide = false
	part.Anchored = true
	part.Material = Enum.Material.SmoothPlastic
	part.Color = Color3.fromRGB(0, 0, 255)
	part.Transparency = transparency -- This.
	part.Parent = workspace
end
```

Great! Now our function can accept whatever number we pass at it, and it'll spawn the part with a transparency of that number - now we just need to pass a number to the function and call it.

## Arguments
When you call a function that contains parameters, you'll have to pass the relevant values into those calls.

```lua
SpawnPart(0.5) -- spawns a part with 0.5 transparency.
SpawnPart(1) -- spawns a part with 1 transparency.
SpawnPart(0.2) -- spawns a part with 0.2 transparency.
SpawnPart(0) -- spawns a part with 0 transparency.
```

These relevant values are called arguments. You define parameters for your functions, and you pass arguments to them. 

Ideally you should match the same amount of arguments as the amount of parameters - if your function has 3 parameters, you should provide 3 arguments to your function calls.

**NOTE:** While you can choose not to pass any arguments to a function that requires them, that value will be `nil`. Be wary of this since your code may error if parts of it do not accept `nil` as a value.

## Returning Values
Sometimes you want your functions to return you a value after it's done. For example, you want a function that can calculate the sum of 2 numbers you pass into it as arguments. After that, you'd want the result of the addition.

This is where `return` comes in. 

```lua
local function Add(num1, num2)
	local result = num1 + num2
	return result
end

local number = Add(1, 2)
print(number)

-- Output:
-- 3
```

You can do a lot more stuff with `return` too. Taking the part spawn example, what if we want to directly access the resulting part that got spawned by our function? We can actually return the part itself.

```lua
local function SpawnPart()
	local part = Instance.new("Part")
	part.CanCollide = false
	part.Anchored = true
	part.Material = Enum.Material.SmoothPlastic
	part.Color = Color3.fromRGB(0, 0, 255)
	part.Transparency = 0.5
	part.Parent = workspace

	return part
end

local part = SpawnPart()
print(part.Transparency)

-- Output:
-- 0.5
```

**WARNING:** Any code after `return` will not run - that is considered unreachable code, causing it to error.

## The Power of Functions
As we have seen, functions are super powerful since it encapsulates code - by condensing all these instructions into a single function that you can run in a single line, code becomes far more editable and less repetitive. This effect stacks too as you use those instructions more often!

There are actually far more intricacies to functions, and we have articles detailing about them - head over to the Scripting section under the Articles folder for more!

## Closing
This article was originally written by Willie, vetted by Remi, and edited for brevity by Valkyria.

Have a suggestion to improve this article? Ping me on Discord! @valkyria#0001