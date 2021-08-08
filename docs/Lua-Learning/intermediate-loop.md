---
title: Intermediates about Loops
---

# Pre-requisites
This guide assumes you have already read the guide for basics about loops. You are also expected to understand about tables and `if` statements - you may face difficulty in understanding this article otherwise.

# More about Loops
In the basics about loops guide, we've talked about some of the loops including `for`, `while` and `repeat`. 

This guide will cover more on loop manipulation, and some of the other loop variants you can use in your projects.

## Generic for loops
Generic `for` loops involve the use of `pairs`/`ipairs`, allowing you to loop through a table.
This is known as iterating through a table - if you have many tables to iterate through, having generic `for` loops make everything that much cleaner.

```lua
local array = { "H", "e", "l", "l", "o" }

for i, v in ipairs(array) do
	print(i .. " - " .. v)
end

-- Output:
-- 1 - H
-- 2 - e
-- 3 - l
-- 4 - l
-- 5 - o
```
```lua
local dictionary = 
	{
		["One"] = 1,
		["Two"] = 2,
		["Three"] = 3,
		["Four"] = 4,
		["Five"] = 5
	}

for k, v in pairs(dictionary) do
	print(k .. " - " .. v)
end

-- Output:
-- Two - 2
-- One - 1
-- Four - 4
-- Five - 5
-- Three - 3
```

Recall what we have went through about `for` loops in the previous guide. This is actually the equivalent to writing:

```lua
local array = { "H", "e", "l", "l", "o" }

for i = 1, #array do -- # returns the length of a table.
	print(i .. " - " .. array[i])
end

-- Output:
-- 1 - H
-- 2 - e
-- 3 - l
-- 4 - l
-- 5 - o
```

## ipairs vs pairs
You may have noticed two things from our examples above:
* The first example uses an array, and uses `ipairs`. The second example uses a dictionary, and uses `pairs`.
* The first example prints values in a numeric fashion. The second example, meanwhile, have a messed up order.

It may not be instinctive at first, but `ipairs` and `pairs` function differently.
* `pairs` return key-value pairs (eg: key "One" - value "1"). Because keys can be unique, sorting can be too expensive. The results can appear to be garbled and unsorted due to this - this reflects the traits of dictionaries, where order does not matter. For this reason, `pairs` are suited for dictionaries.

* `ipairs` return index-value pairs (eg: index 1 - value "H"), starting from the lowest number index to the highest. The side effect to this trait too, is that the results are in a numeric order. Since this only reads numerical indices, and not keys unlike `pairs`, any non-numerical indices in an array gets ignored. These traits mean that `ipairs` are great for arrays.

*In short, use `ipairs` for arrays, and `pairs` for dictionaries.*

## Break
Sometimes you might not want a loop to continue running when a condition is reached WITHIN the loop. 

Consider the example below - right now we want the `for` loop to **stop entirely** when the current value is the same as `myFavoriteValue`. 

```lua
local value
local myFavoriteValue = 3

for i = 1, 5 do
	print(i)
	value = i
end

print("end value: " .. value)

-- Output:
-- 1
-- 2
-- 3
-- 4
-- 5
-- end value: 5
```

We can use an `if` statement and check if `value` is currently under `myFavoriteValue`. If it is, print. If not, stop printing.

```lua
local value = 1
local myFavoriteValue = 3

for i = 1, 5 do
	if i < myFavoriteValue then
		print(i)
	end
	value = i
end

print("end value: " .. value)

-- Output:
-- 1
-- 2
-- end value: 5
```

Internally however, `i` will constantly keep counting up to 5, made evident by the `end value: 5` in the output. We don't want this to happen at all; remember, we want the loop to **stop entirely**.

This is where `break` comes in. You can terminate a loop early with a `break` statement, ignoring to loop after that point and continue on with the script. Let's now apply that to the example:

```lua
local value = 1
local myFavoriteValue = 3

for i = 1, 5 do
	print(i)
	value = i

	if i == myFavoriteValue then
		break
	end
end

print("end value: " .. value)

-- Output:
-- 1
-- 2
-- 3
-- end value: 3
```

Much better. Now, the `for` loop stops counting entirely upon `i` hitting 3.

## Continue
`continue` is also another loop function that you can implement within a loop, just like `break`.

While `break` forces the whole loop to stop repeating and move on with the script, `continue` jumps to the end of the loop, skipping past any code after the `continue` statement. This also does not terminate the loop early, unlike `break`. 

```lua
local myFavoriteValue = 3

for i = 1, 5 do
	if i == myFavoriteValue then
		continue
	end
	print(i)
end

-- Output:
-- 1
-- 2
-- 4
-- 5
```

Notice how `3` is not printed out - when `i` matches `myFavoriteValue`, the `continue` statement is executed, causing the loop to skip the `print(i)` statement while still looping itself afterwards.

Note that `continue` is Luau-exclusive (Roblox implemented this) - vanilla Lua does not have `continue` implemented.

## Closing
Have a suggestion to improve any of the two articles? Ping me on Discord! @valkyria#0001.