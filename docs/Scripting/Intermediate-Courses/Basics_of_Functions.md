---
title: Basics Of Functions
template: docs.html
comments: true
hide:
  - navigation
---

# Functions
I don't like typing a lot of code, you probably don't like typing a lot of code. Wouldn't it be nice if you can compress multiple instructions into 1 line of code? Well, that's what functions are for!

Functions let you run multiple instructions in one line, making your code look more organized and clean, and also making you type less code.

## Defining/Creating Functions
In Luau, defining functions is quite simple. Just follow the template below:
```lua
local function <function_name>()

end
```
Code inside the function is called the *“body”*. The body of a function is executed when the function is called. To call a function, simply type its name followed by parentheses. Something like this:
```lua
local function test_function()
	print("Hello, friends!")
end

test_function()
-- ^ prints "Hello, friends!"
```

## Parameters & Arguments
When defining functions, it's pretty common to have some parameters defined as well. You can think of parameters as variables *exclusive* to that function, a way to pass in some data that the function will use when it is called.
```lua
-- this function has 1 parameter: "name"
local function say_hello(name)
	print("Hello " .. name)
end

say_hello("big dude")
-- ^ prints "Hello big dude"
```

Arguments are data that are passed when calling a function. In the example above, we passed *“big dude”* when calling `say_hello`. Thus, we can say that *“big dude”* is an argument.

If you call a function with fewer arguments than it expects, those missing parameters will be `nil`. If you call a function with more arguments than it expects, it'll ignore those extra arguments.
```lua
local function test_function(parameter_1, parameter_2)
	print(parameter_1, parameter_2)
end

test_function(1) -- fewer arguments
-- ^ prints 1, nil

test_function(1, 2, 3, 4) -- too much arguments
-- ^ prints 1, 2
```

## Return Statements
One of the most useful things a function can do is *returning* data back. Let's say you have a function called `add_these_2_numbers_together` (slick name, I know). As the name suggests, this function adds 2 numbers together and returns the result.
```lua
local function add_these_2_numbers_together(number_1, number_2)
	
end
```
Now obviously we have to… well… add these 2 numbers together.
```lua
local function add_these_2_numbers_together(number_1, number_2)
	local result = number_1 + number_2
end
```
Now, with the hard part over, the last thing we need to do is return the result. We can do this using the conveniently named `return` keyword.
```lua
local function add_these_2_numbers_together(number_1, number_2)
	local result = number_1 + number_2

	return result
end

local sum = add_these_2_numbers_together(1, 2)
print(sum)
-- ^ prints 3 (1 + 2 = 3)
```

Functions can also return multiple values, simply separate the values you want to return with a comma `,`.
```lua
local function add_and_sub(number_1, number_2)
	local sum = number_1 + number_2
	local difference = number_1 - number_2
	
	return sum, difference
end

local value1, value2 = add_and_sub(3, 2)
print(value1)
-- ^ prints 5 (3 + 2 = 5)

print(value2)
-- ^ prints 1 (3 - 2 = 1)
```

**REMEMBER!** You cannot execute code below the `return` keyword because Luau expects an `end` after every `return`. Attempting to do so will result in an error.

## Challenges (Optional)
Here's a challenge for ya!

Make a function that adds, subtracts, and multiplies 2 numbers. Don't forget to return the results!
```lua
local sum, difference, product = add_sub_mult(5, 2)

print(sum)
-- ^ prints 7 (5 + 2 = 7)

print(difference)
-- ^ prints 3 (5 - 2 = 3)

print(product)
-- ^ prints 10 (5 * 2 = 10)
```
??? success "Solution"

    ```lua
	local function add_sub_mult(number_1, number_2)
		local sum = number_1 + number_2
		local difference = number_1 - number_2
		local product = number_1 * number_2
		
		return sum, difference, product
	end
	```


## Closing
Thanks for reading! We hope you've learned a thing or two about functions and how to utilize 'em. Of course, we aren't perfect. We make mistakes, typos, etc. so if you found a mistake while reading this article, or any article for that matter, feel free to [report it](https://rodevs-helpers.github.io/Helpers-Documents/Others/Help_Us%21/), and perhaps you can [review us](https://rodevs-helpers.github.io/Helpers-Documents/Others/Help_Us%21/) too! Any feedback is appreciated. 

Since this article only discussed the basics of functions, here are some resources that dive deeper into functions:

* [Roblox's official documentation](https://create.roblox.com/docs/scripting/luau/functions)
* [Lua PIL “Functions” chapter](https://www.lua.org/pil/5.html)
