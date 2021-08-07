---
title: Variables
---

## Variables? What are those?
You can think of variables as boxes that contains a value. Variables can store anything you want really, you can store numbers, strings, tables, etc.

## Naming variables
In Lua, variable names can be any non-reserved string of letters, digits, and underscores, but they cannot start with a digit:
```lua
local letters -- yes yes good
local coolguy1 -- valid
local snake_case_is_bad -- good
local _variable -- also valid

local if -- no no wtf bad
local 1stCoolGuy -- even worse!!! stop this!!
```
??? info "Lua Keywords"
	Lua keywords like:
	```lua
	if, then, return, break, else, elseif
	```
	**CANNOT** be used for variable names
Since lua is a case-sensitive language, that means ``HIIMJOE`` and ``hiimjoe`` are two completely different variables.

## Assigning
Assigning a value to a variable is quite simple, simply do this

=== "Code"
	```lua
	local coolGuy = "joe"
	local coolnessLevel = 1000000000
	local getsAllTheLadies = true

	print(coolGuy)
	print(coolnessLevel)
	print(getsAllTheLadies)
	```
=== "Output"
	```lua
	joe
	1000000000
	true
	```

You can even assign values to a bunch of variables in one line!!! (crazy ik)

=== "Code"
	```lua
	local coolGuy, coolnessLevel, getsAllTheLadies = "joe", 1000000000, true

	print(coolGuy)
	print(coolnessLevel)
	print(getsAllTheLadies)
	```
=== "Output"
	```lua
	joe
	1000000000
	true
	```

## Local variables vs Global variables
Variables exists in one of two scopes, **local** or **global**.  
All the examples I've provided so far uses **local** variables, you can declare a **global** variable by removing the **local** keyword when declaring a **local** variable.  
So instead of this,
```lua
local hi = 10
```
you'd have this
```lua
hi = 10
```	
A **global** variable can be accessed anywhere in a script. While with **local** variables, you are limited. Here's an example,

=== "Global"
	```lua
	hi = "hey!"
	print(hi) -- "hey!"
	```
=== "Local"
	```lua
	local function kekekekekke()
		local hi = "hey!"
	end
	print(hi) -- wtf is hi?!?!?!?!?!
	```
you can try running both of these seperately, and see what happens ;)

## Thanks for reading !!!!!
Thanks for reading!!! I've been writing this damn article for too long, if there's something missing/wrong, contact me (willie) or one of the senor helpers and we'll fix it. Once again, thanks and peace out.