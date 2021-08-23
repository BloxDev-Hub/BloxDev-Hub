---
title: More About Functions
---
# Intro:
In this guide we will discuss some more stuff about functions. Before proceeding make sure you have some knowledge about function, conditional statements!

# Recursive Function
## What is recursion/recursive function?
Recursion in lua is very simple. In recursion a function calls itself until a condition meets, just like a loop!
Now you must be thinking how a function can call it self?
So there is an example how you can do it!

```lua
local function recursive(n)
  if n == 6 then
    return n
  end
  print(n)
  n = n + 1
  return recursive(n)
end

recursive(1)
```
Output:
```
1
2
3
4
5
```
In the above code we created a recursive function. it first check if the given argument is not 6 then it adds 1 in to it and again call the function.
It repeats the process again and again until the n is equal to 6.

### example:
You can use recursion for lots of stuff. To give you an example I made a recursive function which iterate through an array and print its elements
```lua
local tbl = {"eden","blueberry","roblox","lua","kebabs"}
local function iterator(tb,cur_ind)
   local index = cur_ind or 0
   local value = tb[index+1]
   print(value)
   return tb[index+2] and iterator(index+1)
end

iterator(tbl)
```
Output:

```
eden
blueberry
roblox
lua
kebabs
```

# Anonymous Functions!
## What is an anonymous function?
Anonymous Function are just anonymous, It means that they have no name. We just create them anonymously.
Let me give you an example 
```lua
local function func()
   return function() -- anonymous function
   end
end
```
In the above example the function ``func`` returns an **anonymous function**. You can catche this anonymous function then call it.


# Closure Function!
## What is closure?
Closure could be little complicated but I will try mt best to explain you.
First thing you should always remember is: a `closure function` is an `anonymous function` but an `anonymous function` is not always a `closure functions`.

I will try to explain you with an example!
```lua
local function func()
    local number = 1
    return function()
       number = number +1
       return number
    end
end

local v1 = func()
print(v1())
print(v2())
```
 




