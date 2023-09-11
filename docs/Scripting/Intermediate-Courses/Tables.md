---
title: Understanding the Basics of Tables
template: docs.html
comments: true
hide:
  - navigation
---
# Tables
One of the things you're going to be doing a lot when scripting is handling data and values: *strings*, *numbers*, *booleans*, etc. Wouldn't it be nice to have a way *“encapsulate”* or *“group”* that data together into one single data type?

Introducing tables! Tables let you group data into a single data type. This makes it easier to work with and manipulate data.

## Constructing/Creating Tables
The simplest way to construct a table is by using curly braces `{}`, like this:
```lua
local my_table = {}
```
In Luau, there are 2 kinds of tables: arrays and dictionaries. Arrays are basically lists, like a grocery list or a list of players in a game. Dictionaries are like… well… actual dictionaries! It'll make sense later, I swear!

## Arrays
Arrays use numbers as its indices (known as indexes). Arrays are very useful when it comes to grouping a collection of data, like a group of players that are online or a group of admins in a game.

### Constructing Arrays
To construct an array, simply declare the values you'd like to put in curly braces `{}` separated by commas `,`:
```lua
local top_5_friends = {"Eden", "Joe", "John", "Teerach", "Shogus"}
```

### Reading Arrays
Now, say we want to see who's first in our *“Top 5 Friends”* list. All we need to do is add square brackets `[]` after our `top_5_friends` variable and the entry's position `[position]`. In our case, that position will be `1` since we're checking who's first.
```lua
local top_5_friends = {"Eden", "Joe", "John", "Teerach", "Shogus"}

print(top_5_friends[1])
-- ^ prints "Eden"
```

!!! info


	Unlike other languages, arrays in Luau start at `1` instead of `0`. If we were to do the same thing in another language, for example Ruby, we'd have to do:
	```lua
	top_5_friends[0]
	```

### Writing Into Arrays
To append a new entry to an array, we can use a method from Luau's [`table` library](https://create.roblox.com/docs/reference/engine/libraries/table) called `insert`. Call the method and pass our array's reference `(top_5_friends)` and the value we want to append:
```lua
local top_5_friends = {"Eden", "Joe", "John", "Teerach", "Shogus"}

table.insert(top_5_friends, "Willie")
print(top_5_friends[6]) -- we check the 6th entry because our array has 6 entries
-- ^ prints "Willie"
```
You can also specify where to append by passing in a number when calling `table.insert`. But remember, this method _**will**_ shift any following entries up by one position:
```lua
local top_5_friends = {"Eden", "Joe", "John", "Teerach", "Shogus"}
print(top_5_friends[2])
-- ^ prints "Joe"
print(top_5_friends[3])
-- ^ prints "John"

table.insert(top_5_friends, 2, "Willie")
print(top_5_friends[2])
-- ^ prints "Willie"
print(top_5_friends[3])
-- ^ prints "Joe"

-- the method shifted "Joe" from 2nd to 3rd
```

To overwrite an array's entry, simply put the entry's position in square brackets `[position]` followed by `=` and the new value:
```lua
local list = {"John", "Jonathan", "Joe"}
print(list[3])
-- ^ prints "Joe"

list[3] = "Jon"
print(list[3])
-- ^ prints "Jon"
```

### Deleting Entries
For deleting entries, we can use another method from the [`table` library](https://create.roblox.com/docs/reference/engine/libraries/table) called `remove`. This method will remove the specified entry and also shifts any following entries one position down. Simply call the method and pass the array's reference and the position of the entry you'd like removed:
```lua
local list = {"Eden", "Gato", "Teerach"}
print(list[2])
-- ^ prints "Gato"

table.remove(list, 2)
print(list[2])
-- ^ prints "Teerach"
-- table.remove moved "Teerach" from 3rd to 2nd
```

## Dictionaries
Like I said earlier, dictionaries in Luau are like actual dictionaries. To prove my point, we're going to invent our own language called *“Helperin”* and we're going to make a *“Helperin Dictionary”*. To start off, we're going to add 2 words to our *“Helperin Dictionary”*: *“Dev Mute”* and *“Off-topic”*. This is what our dictionary is going to look like:

- `Dev Mute` = To mute someone for breaking the guidelines.
- `Off-topic` = Talking about topics not relevant to the channel's purpose

Simple enough right? Now, unlike arrays, a dictionary's indices (known as keys) can be literally anything: `strings`, `numbers`, `functions`, etc. For this article, we're going to be using strings exclusively. Mainly because it's the easiest to understand and the simplest one to use.

### Constructing Dictionaries
To construct a dictionary, simply declare each key followed by `=` and the value. Don't forget to separate each key-value pair with commas! `,`. Let's make our *"Helperin Dictionary"*!
```lua
local helperin_dictionary = {
	["Dev Mute"] = "To mute someone for breaking the guidelines",
	["Off-topic"] = "Talking about topics not relevant to the channel's purpose",
}
```

### Reading Dictionaries
Reading from dictionaries is quite simple, add a pair of square brackets `[]` after your dictionary's reference, and inside it, specify the key you want to read from `reference[key]`:
```lua
local helperin_dictionary = {
	["Dev Mute"] = "To mute someone for breaking the guidelines",
	["Off-topic"] = "Talking about topics not relevant to the channel's purpose",
}

print(helperin_dictionary["Dev Mute"])
-- ^ prints "To mute someone for breaking the guidelines"
```
Or if you have a variable:
```lua
local helperin_dictionary = {
	["Dev Mute"] = "To mute someone for breaking the guidelines",
	["Off-topic"] = "Talking about topics not relevant to the channel's purpose",
}

local word = "Off-topic"
print(helperin_dictionary[word])
-- ^ prints "Talking about topics not relevant to the channel's purpose"
```

### Writing into Dictionaries
Now, I want to add a new word to our *“Helperin Dictionary”*. To add a new entry to a dictionary, specify the key you want to add followed by `=` and the new value:
```lua
local helperin_dictionary = {
	["Dev Mute"] = "To mute someone for breaking the guidelines",
	["Off-topic"] = "Talking about topics not relevant to the channel's purpose",
}

helperin_dictionary[">tag joe"] = "A humorous image designed to bully every beginner in existence"

print(helperin_dictionary[">tag joe"])
-- ^ prints "A humorous image designed to bully every beginner in existence"
```
If you want to overwrite an entry in your dictionary, simply do what you just previously did (yes, really):
```lua
local helperin_dictionary = {
	["Dev Mute"] = "To mute someone for breaking the guidelines",
	["Off-topic"] = "Talking about topics not relevant to the channel's purpose",
	[">tag joe"] = "A humorous image designed to bully every beginner in existence"
}
print(helperin_dictionary["Dev Mute"])
-- ^ prints "To mute someone for breaking the guidelines"

helperin_dictionary["Dev Mute"] = "Muting someone from the development category"
print(helperin_dictionary["Dev Mute"])
-- ^ prints "Muting someone from the development category"
```

### Removing Entries
Removing an entry is the same as writing into dictionaries, but instead of assigning a new value to the key, you assign `nil`. Doing this will remove the entry from your dictionary:
```lua
local helperin_dictionary = {
	["Dev Mute"] = "To mute someone for breaking the guidelines",
	["Off-topic"] = "Talking about topics not relevant to the channel's purpose",
	[">tag joe"] = "A humorous image designed to bully every beginner in existence"
}

helperin_dictionary["Dev Mute"] = nil
print(helperin_dictionary["Dev Mute"])
-- ^ prints nil
```

## Iterating Through Tables
Reading a single entry of a table is cool and all, but reading all the entries is cooler. We can do this by iterating through the table using Luau's generalized iterator. Luau's generalized iterator looks like this:
```lua
for index, value in table_name do

end
```
Now, if we want to iterate through an array or a dictionary, we can just use this generalized iterator to do it:
```lua
local friends_list = {"Eden", "Willi", "Shogus"}

for index, friend in friends_list do
	print("Hello! " .. friend)
end
-- ^ prints:
-- Hello! Eden
-- Hello! Willi
-- Hello! Shogus

local student_math_test_scores = {
	["John"] = 98,
	["Laura"] = 80,
	["Janet"] = 78,
	["Larry"] = 40
}

for student, score in student_math_test_scores do
	print(student .. ": " .. score)
end
-- ^ prints
-- Laura: 80
-- Janet: 78
-- John: 98
-- Larry: 40
```

Or you can use good ol' iterator functions: `pairs()` and `ipairs()`. `pairs()` for dictionaries, and `ipairs()` for arrays.
```lua
local friends_list = {"Eden", "Willi", "Shogus"}

for index, friend in ipairs(friends_list) do
	print("Hello! " .. friend)
end
-- ^ prints:
-- Hello! Eden
-- Hello! Willi
-- Hello! Shogus

local student_math_test_scores = {
	["John"] = 98,
	["Laura"] = 80,
	["Janet"] = 78,
	["Larry"] = 40
}

for student, score in pairs(student_math_test_scores) do
	print(student .. ": " .. score)
end
-- ^ prints
-- Laura: 80
-- Janet: 78
-- John: 98
-- Larry: 40
```

!!! warning "THERE'S NO ORDER?!"

	When iterating through dictionaries, you might've realized that it's not ordered correctly. This is because there's no sense of order in dictionaries, unlike arrays which are ordered lists. So be wary of that next time you iterate through a dictionary!

## Challenges (Optional)
Here's a fun challenge! Remember the *"Helperin Dictionary”*? I want you to add new words, edit definitions of existing words, and delete some entries. Personalize it to your liking!
```lua
local helperin_dictionary = {
	["Dev Mute"] = "To mute someone for breaking the guidelines",
	["Off-topic"] = "Talking about topics not relevant to the channel's purpose",
	[">tag joe"] = "A humorous image designed to bully every beginner in existence"
}
```

## Closing
Ayo! Thanks for reading! If there are any mistakes, or maybe you felt like something was missing, [report it](https://rodevs-helpers.github.io/Helpers-Documents/Others/Help%20Us%21/)! If you have some free time, perhaps leave us [a review](https://rodevs-helpers.github.io/Helpers-Documents/Others/Help_Us%21/)! Your feedback means a lot to us and helps us improve our site.
