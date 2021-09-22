---
title: Lua Globals
---

# Global Functions
Global functions in lua are the built-in funcions which are pre declared and are very useful.
There are many of them but in this guide we will discuss some common global functions.

## tonumber()
``tonumber(value,base)``
It converts the given argument in to a ``number`` of desired base (between 2-32). If second argument is missing then by default it converts the given argument into a number of base 10. In case of failure will return ``nil``.
### Example Code:
=== "Code"
	```lua
	print(tonumber("123"))
    print(tonumber("911"))
    print(tonumber("abc"))
	```
=== "Output"
	```lua
	 123
     911
     nil
	```

## tostring()
``tostring(value)``
It converts the given argument in to a ``string``. Just like ``tonumber()``, If it cannot convert it will return ``nil``.
### Example Code:
=== "Code"
	```lua
	print("The statement was".. tostring(true))
    print("Square of 16 is : ".. tostring(16^2))
	```
=== "Output"
	```lua
	 The statement wastrue
     Square of 16 is : 256
	```

## print()
``print(value)``
It takes multiple arguments and display them in the console/output. In most cases it is used for debugging.
### Example Code:
=== "Code"
	```lua
	print("Eden is smart")
    print("Helpers are the best")
	```
=== "Output"
	```lua
	 Eden is smart
     Helpers are the best
	```

## assert()
``assert(statement,error message)
It stops the thread and returns the error message if the given statement is ``false`` or ``nil``.
### Example Code:
=== "Code"
	```lua
	local eden =  "Brilliant"
    assert(eden == "noob", "eden is not noob")
	```
=== "Output"
	```lua
	 eden is not noob
	```

## error()
``error(message)``
It stops the curent thread and gives the error in the output/console.
### Example Code:
=== "Code"
	```lua
	error("Program terminated!")
	```
=== "Output"
	```lua
	 Program terminated!
	```

## type()
``type(value)``
It returns the type of the given argument.
### Example Code:
=== "Code"
	```lua
	local hi = true
    local data = {"Edenroose","Teddy","Cake","Selfish"}
    print(type(hi))
    print(type(data))
	```
=== "Output"
	```lua
	 boolean
     table
	```

## pcall()
``pcall(function)``
It calls the given function in protected mode. In case of any error the thread will not be terminated. ``pcall`` return two values. The first returned value is a bool which is either `true` or `false` depends if the call succeeded or not. If the call succeed then first value will be true and second value will be the value returned by the function called in the protected mode. If the call could not succeed then pcall will return false with the error message.
### Example Code:
=== "Code"
	```lua
	local function test(name)
	    print(name)
	    assert(name == "Edenroose", "Incorrect Name!")
    end
    local status , result = pcall(test("Willie"))
    print(status,result)
	```
=== "Output"
	```lua
	 Incorrect Name!
     table
	```

## unpack()
``unpack(table,initial_index,final_index)``
It returns elements of a table in the form of `tuple`, according to the given arguments. By default: initial_index = 1
final_index = #table
### Example Code:
=== "Code"
	```lua
	local tbl = {"Edenroose","Teddy","Cake","Selfish","Smart","Intelligent"}
    print(unpack(tbl,2,5))
	```
=== "Output"
	```lua
	  Teddy Cake Selfish Smart
     table
	```
## select()
``select(n,args)``
If n is positive, It returns all the given arguments after the index n
If n is negative, It returns all the given n number of arguments from the end
if n is `#` operator, It returns the number of given arguments
### Example Code:
=== "Code"
	```lua
	print(select("#","hi","good","ok","wow","yep"))
	```
=== "Output"
	```lua
	  5
	```
## rawequal()
``rawequal(value1,value2)``
It returns a bool value. If given arguments are equal, it returns `true`. If the arguments are not equal, it returns false
### Example Code:
=== "Code"
	```lua
	print(rawequal(2,2))
	```
=== "Output"
	```lua
	 true
	```

## Thanks For Reading :)
In case of any mistake feel free to contact me via discord "EDENROOSE#1630" .
