---
title: Understanding Tables
---

 [1]: https://developer.roblox.com/en-us/articles/Table
 [2]: https://developer.roblox.com/en-us/api-reference/lua-docs/table
 [3]: https://developer.roblox.com/en-us/articles/String


## What's a table?

[Tables][1] are a data type that can hold multiple values ([Numbers](https://developer.roblox.com/en-us/articles/Numbers), [booleans](https://developer.roblox.com/en-us/articles/Numbers), [strings][3], and more). Creating a table is actually pretty easy, there are ways to create a table, the most common way to create one is by using curly braces ``{}``

=== "Code"
	```lua
	local newTable = {}
	print(type(newTable))
	```
=== "Output"
	```lua
	table
	```

## Arrays and Dictionaries

### Arrays

#### What's an array?

Arrays are basically lists. Let's say you need a list of players in the game, you would need an array to do that. 

#### How do I create one?

Creating arrays is very simple, just store the values and separate each one with a comma ``,`` or a semicolon ``;``.

=== "Code"
	```lua
	local coolDudesList = {"joe", "willie", "jim", "guy in >tag joe"}
	print(coolDudesList)
	```
=== "Output"
	```lua
	{
		[1] = "joe",
		[2] = "willie",
		[3] = "jim",
		[4] = "guy in >tag joe"
	}
	```

#### Reading

Let's say you want to see who the 2nd dude is in the coolDudesList. All you need to do is index the array with a number. Since we want to see the 2nd dude, we'll index the coolDudesList array with the number 2.

=== "Code"
	```lua
	local coolDudesList = {"joe", "willie", "jim", "guy in >tag joe"}
	print(coolDudesList[2])
	```
=== "Output"
	```
	willie
	```

Now we know that the 2nd dude in the list is willie.

#### Writing

Turns out willie is a backstabbing snake and we want to kick him out of the coolDudesList and replace him with remi, we can do that by setting a new value to the 2nd index (Since willie is 2nd in the coolDudesList) like this.

=== "Code"
	```lua
	local coolDudesList = {"joe", "willie", "jim", "guy in >tag joe"}
	coolDudesList[2] = "remi"
	print(coolDudesList[2])
	```
=== "Output"
	```
	remi
	```
Now we have replaced willie with remi.

#### Inserting

ana wants to join coolDudesList. We can insert her name to the coolDudesList by doing this.

=== "Code"
	```lua
	local coolDudesList = {"joe", "remi", "jim", "guy in >tag joe"}
	table.insert(coolDudeList, "ana")
	print(coolDudesList[5])
	print(coolDudesList)
	```
=== "Output"
	```lua
	ana
	{
		[1] = "joe",
		[2] = "remi",
		[3] = "jim",
		[4] = "guy in >tag joe",
		[5] = "ana"
	}
	```
Now we have added a new member to the coolDudesList.

??? info "The # operator"
	In the example above, I used the # operator. If used on an array, it will give you the number of elements in the array. If used on a string, it will give you the amount of characters in that string
	=== "Code"
		```lua
		print(#"Hi".." characters")
		print(#{"hi", "hey", "hiiiii", "heyyyyyyy"}.." elements")
		```
	=== "Output"
		```lua
		2 characters
		4 elements
		```

#### Removing

After being in the list for some time. joe decided to leave the coolDudesList to pursue other endeavors. We can remove him from the list by doing this.

=== "Code"
	```lua
	local coolDudesList = {"joe", "remi", "jim", "guy in >tag joe", "ana"}
	coolDudesList[1] = nil
	print(coolDudesList[1])
	print(coolDudesList)
	```
=== "Output"
	```lua
	nil
	{
		[1] = void
		[2] = "remi",
		[3] = "jim",
		[4] = "guy in >tag joe",
		[5] = "ana"
	}
	```

But now, we have a problem, the 1st index is now void, which can be unfavourable in some situations. To avoid this we can use the remove function provided by the [table][2] lib

table.remove(array, position) takes 2 arguments, the array, and the position. What's cool about this function is it shifts down the rest of the elements in the array. If you didn't understand what I just said, here's a drawing I made in 5 minutes.

<img src=https://github.com/Rodevs-Helpers/Helpers-Documents/blob/editing/images/table.remove.png?raw=true width="500" height="500"/>

You see how the names shifts down, so remi becomes 1st dude, jim becomes the 2nd, etc.

=== "Code"
	```lua
	local coolDudesList = {"joe", "remi", "jim", "guy in >tag joe", "ana"}
	table.remove(coolDudesList, 1)
	print(coolDudesList)
	```
=== "Output"
	```lua
	{
		[1] = "remi",
		[2] = "jim",
		[3] = "guy in >tag joe",
		[4] = "ana"
	}
	```

Now as you can see, there's no more void!

### Dictionaries

Dictionaries are arrays that are indexed with [strings][3], not numbers.
So instead of this.
```lua
local coolDudesList = {"remi", "jim", "guy in >tag joe", "ana"}
```
You'd have this.
```lua
local dict = {
	["coolguy1"] = "remi",
	["coolguy2"] = "jim",
}
```

Let's say we have a dictionary of people's statuses
```lua
local statuses = {
	["remi"] = "Cool",
	["jim"] = "Cool",
	["guy in >tag joe"] = "Cool",
	["ana"] = "Cool"
}
```

#### Reading

Let's say we want to check remi's status and see if he's still cool, we can easily do that by doing this
=== "Code"
	```lua
	local statuses = {
		["remi"] = "Cool",
		["jim"] = "Cool",
		["guy in >tag joe"] = "Cool",
		["ana"] = "Cool"
	}

	local remiStatus = statuses["remi"]
	print(remiStatus)
	```
=== "Output"
	```
	Cool
	```

??? info "Indexing dictionaries"
	When indexing dictionaries you can use the dot operator ``(.)``, or you can use square brackets ``[]``
	```lua
	--same thing :))
	local remiStatus1 = statuses["remi"]
	local remiStatus2 = statuses.remi
	```

#### Writing

After checking all the statuses, we concluded that jim isn't really that cool anymore. To change his status, we can just do this.
=== "Code"
	```lua
		local statuses = {
		["remi"] = "Cool",
		["jim"] = "Cool",
		["guy in >tag joe"] = "Cool",
		["ana"] = "Cool"
	}

	statuses["jim"] = "Uncool"
	print(statuses["jim"])
	```
=== "Output"
	```lua
	Uncool
	```

#### Removing

After finding out that jim isn't really that cool anymore. We decided to kick him out of the group.
=== "Code"
	```lua
		local statuses = {
		["remi"] = "Cool",
		["jim"] = "Uncool",
		["guy in >tag joe"] = "Cool",
		["ana"] = "Cool"
	}

	statuses["jim"] = nil
	print(statuses)
	```
=== "Output"
	```lua
	{
		["remi"] = "Cool",
		["guy in >tag joe"] = "Cool",
		["ana"] = "Cool"
	}
	```

## Iterating over tables

Iterating over tables is one of the easiest things in scripting. In this section, I will guide on what functions to use and when to use them.

### Iterating over arrays

When iterating over arrays you can use a numerical for loop, the ipairs function, or the pairs function.

=== "Numerical for loop"
	```lua
	local array = {"a", "b", "c", 1}
	for index = 1, #array do
		local value = array[index]
		print("Index: "..index, "Value: "..value)
	end
	```
=== "Ipairs function"
	```lua
	local array = {"a", "b", "c", 1}
	for index, value in ipairs(array) do
		print("Index: "..index, "Value: "..value)
	end
	```
=== "Pairs function"
	```lua
	local array = {"a", "b", "c", 1}
	for index, value in ipairs(array) do
		print("Index: "..index, "Value: "..value)
	end
	```

Output:
```
Index: 1  Value: a
Index: 2  Value: b
Index: 3  Value: c
Index: 4  Value: 1
```

### Iterating over dictionaries
You can use the pairs() function to iterate over dictionaries, though it won't loop in order, so be wary of that when you iterate over dictionaries.

=== "Code"
	```lua
	local dict = {
		["joe"] = "cool",
		["remi"] = "kinda cool",
		["jimmy"] = "who?"
	}
	for index, value in pairs(dict) do
		print("Index: "..index, "Value: "..value)
	end
	```
=== "Output"
	```lua
	Index: remi  Value: kinda cool
	Index: joe   Value: cool
	Index: jimmy Value: who?
	```

## Thanks for reading!!!!
Big thanks for reading this article, there are some things that I glossed over for the sake of making this article not long and boring.

Here are some links to learn more about tables.

* [Devhub's article on tables][1]
* [Devhub's article on the table lib][2]

Hope you now understand what tables are and how to use them.
