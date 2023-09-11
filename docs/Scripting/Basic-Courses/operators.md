---
title: What Are Operators?
template: docs.html
comments: true
hide:
  - navigation
---

## Operators
Operators are a set of symbols that you can use to do *cool* and *quirky* things.

## Logical operators
The logical operators are ``#!lua and``, ``#!lua or``, ``#!lua not``.
These operators considers ``false`` and ``nil`` as "false" and everything else as "true".

### And
``and`` will evaluate as ``true`` if both conditions are ``true``

=== "Code"
	```lua
	local trueStatement = (1 + 1 == 2) and (3 * 2 == 6)
	local falseStatement = (2 - 1 == 1) and (6 / 2 == 5)

	print(trueStatement)
	print(falseStatement)
	```
=== "Output"
	```
	true
	false
	```

You can also use ``and`` to check a condition when assigning a value to a variable without using an if statement.

=== "Code"
	```lua
	local rightAnswer = (2 + 2 == 4) and "right"
	-- Since 2 + 2 is indeed 4, it will assign "right" to rightAnswer

	print(rightAnswer)
	```
=== "Output"
	```lua
	right
	```

### Or
``or`` will evaluate as ``true`` if one of the conditions are ``true``

=== "Code"
	```lua
	local trueStatement = (2 + 2 == 69) or (2 * 2 == 4)
	-- One of these conditions are true, hence it will evaluate as true

	local falseStatement = (6 ^ 6 == 89) or (2 - 9 == -420)
	-- Both conditions are false, hence it will evaluate as false

	print(trueStatement)
	print(falseStatement)
	```
=== "Output"
	```
	true
	false
	```
Just like ``and``, you can also use ``or`` when assigning values to variables.

=== "Code"
	```lua
	local answer = (2 + 2 == 5) and "right" or "wtf wrong !!!!"
	--[[ Since 2 + 2 is not 5, it will assign "wtf wrong !!!!" to answer, 
	instead of assigning "right" to it.
	]]

	print(answer)
	```
=== "Output"
	```
	wtf wrong !!!!
	```

### Not
``not`` will evaluate as the opposite of the condition. For example, ``not true --> false``, ``not false --> true``

=== "Code"
	```lua
	local trueStatement = (2 + 2 == 4) -- true
	local falseStatement = (2 + 2 == 5) -- false

	print(not trueStatement)
	print(not falseStatement)
	```

=== "Output"
	```
	false
	true
	```

## Relational
Relational operators are used to compare 2 values and will return a [boolean](https://developer.roblox.com/en-us/articles/Boolean) (``true`` or ``false``)

### Equal to (==)
As the name suggests, this operator checks if one value is equal to another value.

=== "Code"
	```lua
	print(2 == 1 + 1)
	print(3 == 2)
	```
=== "Output"
	```lua
	true
	false
	```

### Not equal to (~=)
This operator checks if one value does not equal to another value

=== "Code"
	```lua
	print("joe" ~= "willie")
	print(1 ~= 0 + 1)
	```
=== "Output"
	```
	true
	false
	```

### Greater than (>)
This operator checks if one value is greater than to another value

=== "Code"
	```lua
	print(3 > 2)
	print(-1 > 4)
	```
=== "Output"
	```
	true
	false
	```

### Less than (<)
This operator checks if one value is less than to another value

=== "Code"
	```lua
	print(2 < 3)
	print(4 < -1)
	```
=== "Output"
	```
	true
	false
	```

### Greater than or equal to (>=)
This operator checks if one value is great than or equal to to another value

=== "Code"
	```lua
	print(3 >= 1)
	print(3 >= 3)
	print(3 >= 5)
	```
=== "Output"
	```
	true
	true
	false
	```
### Less than or equal to (<=)
This operator checks if one value is less than or equal to to another value

=== "Code"
	```lua
	print(1 <= 3)
	print(1 <= 1)
	print(5 <= 3)
	```
=== "Output"
	```
	true
	true
	false
	```

## Arithmetic
Lua supports the usual binary operators along with exponentiation (^), modulus (%), and unary negation (-). These are pretty self explanatory, so I won't be providing any explanations.

### Addition (+)

=== "Code"
	```lua
	print(2 + 2)
	print(3 + 6)
	```
=== "Output"
	```lua
	4
	9
	```

### Subtraction (-)

=== "Code"
	```lua
	print(4 - 2)
	print(5 - 2)
	```
=== "Output"
	```lua
	2
	3
	```

### Multiplication (*)

=== "Code"
	```lua
	print(2 * 3)
	print(3 * 3)
	```
=== "Output"
	```lua
	6
	9
	```

### Division (/)

=== "Code"
	```lua
	print(6 / 2)
	print(1 / 2)
	```
=== "Output"
	```lua
	3
	0.5
	```

### Exponentiation (^)

=== "Code"
	```lua
	print(2 ^ 3)
	print(3 ^ 3)
	```
=== "Output"
	```lua
	8
	27
	```

### Modulus (%)

=== "Code"
	```lua
	print(2 % 2)
	print(13 % 6)
	```
=== "Output"
	```lua
	0
	1
	```

### Unary negation (-)

=== "Code"
	```lua
	print(-4)
	```
=== "Output"
	```lua
	-4
	```

## Miscellaneous
Miscellaneous operators include *concatenation* and *length*.

### Concatenation (..)
Concatenates 2 values together. You can only concatenate **strings** and **numbers**

=== "Code"
	```lua
	print("hello ".."world!!!!")
	```
=== "Output"
	```lua
	hello world!!!!
	```

### Length (#)
If used on a table, specifically an *array*, it will return the number of elements in that array. If used on a *string*, it will return the amount of characters in that string, *spaces are counted too*

=== "Code"
	```lua
	local array = {1,5,6,8,9}
	local leString = "hellooo"
	print(#array)
	print(#leString)
	```
=== "Output"
	```
	5
	7
	```

## Thanks for reading !!!
If there are any mistakes found in this article, please report the artcile!