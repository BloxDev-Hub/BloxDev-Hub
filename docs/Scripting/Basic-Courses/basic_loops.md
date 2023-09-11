---
title: Basics about Loops
template: docs.html
comments: true
hide:
  - navigation


---

# Loops in Lua
Sooner or later while scripting, you will have to repeat instructions for your game to run - you do not want to have to constantly copy the instruction you want to keep running.

This is where loops come in. Loops allow you to repeat a set of instructions to your game with none of the copy-paste nightmare. It also keeps your code organized and clean.

## Types of loops
In Lua, there are multiple types of loops that you may use. They fill different niches, and you may have to use them for different occasions.

```lua
while wait(1) do print("deden") end -- 'while' loop.
for deden = 0, 20 do print("deden") end -- 'for' loop.
repeat deden = deden + 1 until deden < 20 -- 'repeat' loop.
```

## While Loops
`while` loops first check the condition given. If the condition is true, it runs its code. This will repeat for as long as the condition remains true.
Notice how the example below stops working when `i` is 5.

=== "Code"
	```lua
	local i = 0
	while i < 5 do
		print(i)
		i = i + 1
	end
	```
=== "Output"
	```
	1
	2
	3
	4
	```

!!! warning ""
	 `while` loops run for as long as the condition is true; if your condition remains true without changing and without a `wait()`, your `while` loop runs forever and will cause your game to hang. This is known as an infinite loop - avoid this at all costs.

## For Loops
Given a number known as the counter, `for` loops repeat for as long as the counter does not hit the given maximum.

=== "Code"
	```lua
	for i = 1, 5 do
		print(i)
	end
	```
=== "Output"
	```
	1
	2
	3
	4
	5
	```

You may have noticed that `for` loops look very similarly to `while` loops. Consider that the `for` loop example runs similarly to the `while` loop example.

## For loop increments
Notice how we used only 2 numbers in the statement `for i = 1, 5 do`. When you provide 2 numbers, the `for` loop in question will assume you are attempting to count up by increments of 1 `(1, 2, 3, 4, 5)`. 

You can override this behavior by providing a 3rd number, otherwise known as the increment. When you do so, your loop will instead start counting up in that increment.

=== "Code"
	```lua
	for i = 1, 5, 2 do
		print(i)
	end
	```
=== "Output"
	```
	1
	3
	5
	```

In the example below, we have provided `2` as the increment. This tells the `for` loop to start counting up by 2 instead of the default 1. 

You can even apply this to have your `for` loop count DOWNWARDS.

=== "Code"
	```lua
	for i = 5, 1, -1 do
		print(i)
	end
	```
=== "Output"
	```
	5
	4
	3
	2
	1
	```

!!! warning
	An increment of 0 results in an infinite loop as the `for` loop never reaches the end value!

## Repeat loops
`repeat` loops run the code, and then checks if the `until` condition is true. If it is NOT true, the loop repeats until the condition is true.
This behaves very similarly to a `while` loop. However, a `while` loop checks its condition first. A `repeat` loop runs the code first, before checking its condition.

A good way of phrasing this will be like so:

* "while this is true, do this" / "check first, then do"
* "repeat doing this until this is true" / "do first, then check"

=== "Code"
	```lua
	local i = 0
	repeat 
		i = i + 1
		print(i)
	until i > 5
	```
=== "Output"
	```
	1
	2
	3 
	4 
	5 
	6
	```

!!! note ""
	* Notice the inequality sign (>) in the until statement.
 	* This can be interpreted as "add 1 to i, then check if i is above 5. If yes, don't repeat anymore. Else, repeat."

=== "Code"
	```lua
	local i = 0
	while i < 5 do
		i = i + 1
		print(i)
	end
	```
=== "Output"
	```
	1
	2
	3
	4
	5
	```

!!! note ""
	* Notice the inequality sign (<) in the while statement, which is different from that in the repeat loop above.
	* This can be interpreted as "check if i is above 5. If yes, repeat. Else, skip and do not loop anymore."
	* This is also why the while loop doesn't print 6, while the repeat loop does.

## Closing
Loops are very powerful constructs that let you repeatedly run a set of instructions with minimal copy and paste. This makes your code easy to read and edit and also gives you more control over it.

Where applicable, use the appropriate ones as much as possible!