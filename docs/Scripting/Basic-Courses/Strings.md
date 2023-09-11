---
title: Basics Of String
template: docs.html
comments: true
hide:
  - navigation
---
# Strings
Strings are an important part of programming and are used in many high-level programming languages. A string is a combination of alphabetical letters, numbers, and other symbols.

## Declaring String
Strings can be declared in numerous ways however the most commonly used are by using double quotes(") and single quotes(').

```lua
local str = "EdenRose"
local user = 'EdenRose#1968'
```
### Multi-line String
A Multi-line string can be declared by using double brackets (`[[`)

```lua
local str = [[Helpers of Rodevs are very skilled.
They help a lot in development channels.]]

local str2 = [[Helpers are the pride of Rodevs.
They spend their free time helping out others. :) ]]
```

## Concatenation
Concatenation is as method by using which we can combine two strings, for doing so we use "`..`" between both the strings.

=== "Code"
    ```lua
    local str1 = "I am "
    local str2 = "EdenRose"
    print(str1..str2)
    ```

=== "Output"
    ```
    I am EdenRose
    ```

## String Escaping
In a string declared with (") or ('), You can produce almost any character using (`\`). It can be used in many ways such as having quotes inside a string without disturbing it, printing in a new line, etc.

=== "Code"
    ```lua
    print("Greetings \"Rodevs\"")
    print("First line \nSecond line)
    ```
=== "Output"
    ```
    Greetings "Rodevs"
    First line
    Second line
    ```


## Arithmetic With Strings
When using arithmetic operators between strings, Lua tends to convert the string into a number.

=== "Code"
    ```lua
    print("7" + "22")
    print("17" - 4)
    ```
=== "Output"
    ```
    29
    13
    ```

!!! warning
    If Lua failed to convert any string such as "Rose" then it will return an error causing termination of the thread.

## Conversion
A string can be converted into a number by simply using `tonumber()`, a global function of Lua.

=== "Code"
    ```lua
    print(tonumber("78")) 
    print(tonumber("hola"))
    ```
=== "Output"
    ```
    78
    nil
    ```

Similarly, a number can also be converted into a string by the function `tostring()`

=== "Code"
    ```lua
    print(tostring(78))
    ```
=== "Output"
    ```
    78
    ```

## Closing
I hope you had a good time reading this. In case of any mistake please report the article. 