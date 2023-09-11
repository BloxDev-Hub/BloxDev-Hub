---
title: More About Functions
template: docs.html
comments: true
hide:
  - navigation
---
# Intro:
In this guide, we will discuss some more stuff about functions. Before proceeding make sure you have some knowledge about the function and conditional statements!

# Recursive Function
## What is recursion/recursive function?
Recursion in Lua is very simple. In recursion, a function calls itself until a condition meets, just like a loop!
Now you must be thinking about how a function can call itself?
So there is an example of how you can do it!

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
In the above code, we created a recursive function. Firstly, it checks if the given argument is not 6 then it adds 1 to it and again calls the function.
It repeats the process again and again until the `n` is equal to 6.

### example:
You can use recursion for lots of stuff. To give you an example I made a recursive function that iterates through an array and prints its elements
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
Anonymous functions are just anonymous, It means that they have no name. We just create them anonymously.
Let me give you an example

```lua
local function func()
   return function() -- anonymous function
   end
end
```

In the above example the function ``func`` returns an **anonymous function**. You can cache this anonymous function and then call it.


# Closure Function!
## What is a closure?
The closure could be a little complicated but I will try my best to explain you.
The first thing you should always remember is: that a `closure function` is an `anonymous function` but an `anonymous function` is not always a `closure function`.

I will try to explain you with an example!
```lua
local function func()
    local number = 2
    return function() -- a closure function
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

Now you might be confused but no worry I will explain you!
So, here are a few points you should know to understand that

1. A closure function always has access to the variables (upvalues) of that function that returned this closure function.
2. If a closure function updates any of those upvalues say it changed the upvalue from `"2"` to `"4"`, now whenever that closure function is called the value will be "4".

Now if you look back on the code you might start understanding how a closure function works.
In the example code, we created the function ``func``. Inside the function, we created a variable ``number`` and store 1 in it. After that, we returned a `closure` function and inside closure, we added 1 in the number variable.

We cached that closure function in a variable `v1`. Now whenever we call it, it adds "1" to the `number` variable. For the first time when we called the closure function, the variable "number" had 2 in it. So, after adding it becomes 3 and returned 3. When the closure function was called for the second time the number variable had 3 in it and after adding it became 4. And that's how a closure function works.

Hope you understand it now. If there is still any confusion try reading it again.
You might be thinking the closure function is a useless thing but if you are thinking that then you are 200% wrong because closure functions are pretty useful and very important.
Using closure you can make cool stuff.
just to show you how much useful they are, I made an iterator function just like ``pairs/ipairs``, and here it is:

```lua
local function iter(b)
   local ins = 0
   local s
   return function()
      ins += 1
      return b[ins] and ins , b[ins]
   end
end
local tbl = {"edenrose", "hi", "cute", "alive"}
for i,v in iter(tbl) do
   print(i,v)
end
```

Output:

```
1 edenrose
2 hi
3 cute
4 alive
```

# Thanks For Reading!
In case of any mistakes, please report the article, and don't forget to leave your reviews!




