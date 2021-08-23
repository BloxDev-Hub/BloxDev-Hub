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
    local number = 2
    return function() -- a closure funcion
       number = number + 1
       return number
    end
end

local v1 = func()
print(v1())
print(v1())
```
 Output:
 ```
 3
 4
 ```
Now you might be confused but no worry I will explain you :)
So, Here are few points you should know in order to understand that.
1) A closure function always have access to the variables (upper values) of that function which returned this closure function.
2) If a closure function update any of those upper values, say it changed the upper value from `"2"` to `"4"`, now when ever that closure function is called the value will be "4".

Now if you look back on the code you might start understanding how a closure function works.
In the example code we created a function ``func``. Inside the function we created a variable ``number`` and store 1 in it. After that we returned a `closure` function and inside closure we added 1 in the number variable.

We cached that closure function in a variable `v1` and called it. Now when ever we call it, it adds "1" in the `number` variable. For the first time when we called the closure function, the variable "number" had 2 in it. So, after addition it becomes 3 and returned 3. When closure function was called for the second time the number variable had 3 in it and after addition it beacomes 4. And thats how a closure function works.

Hope you understand it now. If there s still any confusion try reading it again.
You might be thinking closure function a useless thing but if you are thinking then your are 200% wrong because closure functions are pretty useful and very important.
Using closure you can make cool stuff.
To show you how much usefull they are i made an iterator function just like ``pairs/ipairs``, and here it is:
```lua
local function iter(b)
	local ins = 0
	local s
	return function()
		ins += 1
		return b[ins] and ins , b[ins]
	end
end
local tbl = { "edenroose" ,"hehe","cute","alive"}
for i,v in iter(tbl) do
	print(i,v)
end```
Output:
```
1 edenroose
2 hehe
3 cute
4 alive
```

# Thanks For Reading!
Hope you enjoyed. Incase of any mistake feel free to contact me via discord **"EDENROOSE#1630"**




