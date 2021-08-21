---
title: Variables
---

## Variables
The most important feature in all of programming, variables are containers that can hold a value you want.

In Luau, variables are capable of holding a value of any type, be it a string, number, table, instances or even functions.

## Naming variables
In Luau, variables can be named any way you like, though you might want to follow conventions. There are however, some rules - variables:

* Cannot start off with digits.
* Cannot be named the same as a reserved keyword (e.g: `if`, `while`, `end`).
* Are case-sensitive; `valk` is not the same as `Valk`.

```lua
-- Valid:
local letters
local coolGuy1
local snake_case_is_bad
local _variable
local TestObject

-- Invalid:
local if
local 1stCoolGuy
```

## Assigning variables
Assigning a value to a variable is quite simple, simply do this:

```lua
local coolGuy = "joe"
local coolnessLevel = 1000000000
local getsAllTheLadies = true

print(coolGuy)
print(coolnessLevel)
print(getsAllTheLadies)

-- Output:
-- joe
-- 1000000000
-- true
```

You can even assign values to a bunch of variables in one line. This can be referred to as a tuple.

```lua
local coolGuy, coolnessLevel, getsAllTheLadies = "joe", 1000000000, true
```

## Local variables vs Global variables
Variables exists in one of two scopes, **local** or **global**.
All the examples so far use **local** variables - however, you can declare a global variable by removing the `local` keyword when declaring a local variable.

```lua
local hi = 10 -- A local variable.
bye = 20 -- A global variable.
```

A **global** variable can be accessed anywhere in a script - with **local** variables, you are limited.

```lua
-- Global:
print(e) -- The linter will complain, but this will still print 'valk' as per normal.

if true then
	e = "valk"
end

print(e) 

-- Output:
-- valk
-- valk
```
```lua
-- Local:
if true then
	local e = "valk"
end

--print(e) -- This errors.
```

We will go through this more in another article - Scoping.

**NOTE:** Due to internal reasons, `global` variables are slower for your game to access and modify. They also ruin scoping. Use `local` under all circumstances.

## Closing
This article was originally written by Willie, vetted by Remi, and edited for brevity by Valkyria.

Have a suggestion to improve this article? Ping me on Discord! @valkyria#0001