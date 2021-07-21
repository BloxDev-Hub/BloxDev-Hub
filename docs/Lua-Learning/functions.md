---
title: Functions
---

# Functions in lua
Functions are one of the fundamentals of scripting. It's one of the first things you will learn in scripting. In this article, I will explain what functions are, how to use them, and when to use them.

## What are functions?
You can think of functions as sets of instructions that can be used multiple times. Functions can make your code look neat and readable.

## Defining functions
So here's how you define a function.
```lua
local functionName()
	-- <body>
end
```
*body* is the code that will run when the function is called.  
So let's make our first function, we'll call it **isCool**.
We'll use this function to determine if someone is cool or not.
```lua
local function isCool(name)
	print("hi")
end
```

## Calling functions
Calling a function is pretty simple. You just have to type the function's name followed by ``()``

=== "Code"
	```lua
	local function isCool(name)
		print("hi")
	end

	isCool()
	```
=== "Output"
	```lua
	hi
	```

## Parameters & arguments
When defining functions, you can add parameters.  
Parameters are like substitutes to the arguments that are passed when the function is called.  

When calling functions, you can add things between the parentheses ``()``, those things are what we call arguments.
=== "Code"
	```lua
	local function isCool(name) -- "name" is a parameter
		print(name)
	end

	isCool("joe") -- "joe" is an argument
	```
=== "Output"
	```lua
	joe
	```
In this example, we passed "joe" when calling the function, and as you can see, it prints "joe".

??? warning "nil arguments"
	If the function you called expected more arguments than you provided,
	=== "Code"
		```lua
		local function yes(yes1, yes2)
			print(yes1)
			print(yes2)
		end

		yes("hi")
		```
	=== "Output"
		```lua
		hi
		nil
		```
	all the missing parameters will be nil.

## Returning values
One of the most useful things about functions, is that it can return values when called.
=== "Code"
	```lua
	local function isCool(name) -- "name" is a parameter
		if name == "joe" then
			return "YESSSS"
		else
			return "NOOOOOO"
		end
	end

	local isJoeCool = isCool("joe")
	local isWillieCool = isCool("Willie")
	print(isJoeCool)
	print(isWillieCool)
	```
=== "Output"
	```lua
	YESSSS
	NOOOOOO
	```
One thing to note here, any code after ``return`` will **not** run. It will actually error in lua.
=== "Code"
	```lua
	local function hi()
		print("hi")
		return "hi2"
		print("hi3")
	end

	local isHi = hi()
	print(isHi)
	```
=== "Output"
	```
	input:4: 'end' expected (to close 'function' at line 1) near 'print'
	```

## When to use functions
Let's say we have this blob of code that give texts a "typewriter" effect.
```lua
local text = "heyyyyyy"
local textLabel = thingy.TextLabel
for i = 1, #text do
	textLabel.Text = string.sub(text, 1, i)
	wait(.5)
end
```
Now writing this everytime you want to achieve a "typewriter" effect is pretty boring and redundant. To avoid this, we can turn this code into a function!
```lua
local function typeWriter(textLabel, text, speed)
	for i = 1, #text do
		textLabel.Text = string.sub(text, 1, i)
		wait(speed)
	end
end
```
Now instead of writing that long blob of code, we can just call the typeWrite function! This way, we don't have to write the same long code and it saves time :).

## Thanks for reading !!!!! :)
Big thanks for reading this article, I hope you now know what functions are and how to use them. If you feel like something is missing in this article or you saw some stupid typo, feel free to contact the Misc Manager (me !!), and I'll gladly fix it.  
Here are some links to functions, if you want to learn more about the topic.

* [lua.org's article on functions](https://www.lua.org/pil/5.html)
* [Devhub's article on functions](https://developer.roblox.com/en-us/articles/Function)
