---
title: Utilising Tables
---

 [1]: https://developer.roblox.com/en-us/articles/Table
 [2]: https://developer.roblox.com/en-us/api-reference/lua-docs/table

# Tables on Roblox Scripting

Tables are one of the most commonly used data type in Roblox Scripting and in programming in general. Though utilising tables are quite easy, utilising them right can be a little tricky, especially for beginners. So in this article I will attemp to explain what [tables][1] are and how to use them.

## What's a table?

[Tables][1] are a data type that can hold multiple values ([Numbers](https://developer.roblox.com/en-us/articles/Numbers), [booleans](https://developer.roblox.com/en-us/articles/Numbers), [strings](https://developer.roblox.com/en-us/articles/String), and more). Creating a table is actually pretty easy, there are 2 ways to create a table, the most common way to create one is by using curly braces ``{}``

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

Creating arrays is very simple, just store the values and seperate each one with a comma ``,`` or a semicolon ``;``.

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

#### Reading, writing, inserting, and removing

##### Reading

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

##### Writing

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

##### Inserting

ana wants to join coolDudesList. We can insert her name to the coolDudesList by doing this.

=== "Code"
	```lua
	local coolDudesList = {"joe", "remi", "jim", "guy in >tag joe"}
	coolDudesList[#coolDudesList+1] = "ana"
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

##### Removing

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
But now, we have a problem, the 1st index is now void, which can be unfavourable in some situations. To combat this we can use the remove function provided by the [table][2] lib