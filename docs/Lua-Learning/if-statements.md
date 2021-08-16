---
title: If Statements
---

# If Statements
Perhaps the most used construct in all of programming and scripting, `if` statements let you do stuff **only if** a condition is fulfilled, opening up new ways to define your game logic.

An example of this is if you want your game to only allow players to enter an area *if* his level is above a certain amount.

## How to Use
The clue's actually in the name already - you just write an `if` statement using `if`!
```lua
if true then
    print("valk")
end

-- Output:
-- valk
```

A better way of reading it would be *"if this is true then do this"*. 

## Adding other conditions
Now what if we want our `if` statement to do something else entirely if the first condition is **not** true? That's where `else` comes in.

```lua
local counter = 1 -- Change this to any value you wish.
if counter == 1 then -- == is for comparison. Not to be confused with =, which is for assignment.
	print("counter is 1!")
else
	print("counter is not 1!")
end
```

A better way of reading it would be *"if this is true, do this. or else, do that"*.

However, what if we want our game to run something else if it matches another condition? Use `elseif`!

```lua
local counter = 1 -- Change this to any value you wish.
if counter == 1 then
	print("counter is 1!")
elseif counter == 2 then
	print("counter is 2!")
else
	print("counter is not 1 or 2!")
end
```

A better way of reading it would be *"if this is true, do this. or else if it's something else, do that. or else, do something else entirely."*.

**Note how we did not place an `end` for every `elseif` or `else` block.** If you tried doing this, you'll get a syntax error.

## Examples
Say you want a player to be able to buy something only if he can afford it. A rough sketchup of the code could look something like this:

```lua
local cash = 200
local cost = 100

if cash > cost then
	print("give stuff to player") -- This is just a placeholder.
	cash = cash - cost
end
```

The example I gave above is a pretty strong example for an `if` statement. In reality however, an `if` statement can be used for many more purposes. 

## Closing
Hopefully this guide should help you approach `if` statements more confidently. 

Have a suggestion to improve this article? Ping me on Discord! @valkyria#0001