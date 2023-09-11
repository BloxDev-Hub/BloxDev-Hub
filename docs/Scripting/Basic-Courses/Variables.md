---
title: Declaring Variables
template: docs.html
comments: true
hide:
  - navigation
---

# Variables
A variable is basically a name that can hold values. These values can be [numbers](https://developer.roblox.com/en-us/articles/Numbers), [strings](https://developer.roblox.com/en-us/articles/String), [tables](https://developer.roblox.com/en-us/articles/Tables) and other Roblox [data types](https://developer.roblox.com/en-us/api-reference/data-types).

## Naming Variables
Variable name can contain English letters, numerical digits and underscores. A variable name can start with letters and underscores but can not start with digits. 

!!! success "Correct Names"
    ```
	Eden
	Teerach_Noob
    Rose22
	_Willie
    ```

lua is a **case-sensitive** language. This means, `Eden` and `eden` will be treated as two different variables. Keywords such as `for`, `break`, `true`, `local`, etc can't be utilised as variable names.

!!! fail "Wrong Names"
    ```
	if
    21st_century
    ```

# Assigning Values

The operator `=` is used for assignment of values. Consider the following example

=== "Code"
    ```lua
    sloth = "a lazy animal"
    print(sloth)
    ```
=== "Output"
    ```
    a lazy animal
    ```

A declared variable can be changed anytime by assigning another value to it.

=== "Code"
    ```lua
    Deden = 4
    print(Deden)
    Deden = 17
    print(Deden)
    ```
=== "Output"
    ```
    4
    17
    ```

### Multiple assignment
Lua also enables its users to declare multiple variables at once. It can be done by separating variable names and their values by `,`.

```lua
Salzu, Paper, Eden = "Fox", "China", "Rose"
```
In the above example variables will be assigned values in serial order.

## Scopes
In lua, a variable can be declared in any of the two scopes `local` and `global`.

### Global Variables
Variables declared in global scope is accessible in all the scopes of a script. Every variable by default is a global variable unless declared with the keyword `local`.

=== "Code"
    ```lua
    do -- first scope
      x = 9
      print(x)
    end 

    do -- second scope
     print(x)
    end 
    ``` 
=== "Output"
    ```
    9
    9
    ```

The variable declared in first scope is accessible in second scope.

??? warning
    Because global variables and functions must be accessed by a hash lookup, they can be expensive to use in terms of performance. In fact, a global variable accessed in a time-critical loop can perform 10% slower (or worse) than a local variable in the same loop.
    As noted earlier, global variables and functions are only accessible within the associated script, not between multiple scripts.

### Local Variables
Local variables are declared with the keyword `local` and are only accessible in the scope in which they are defined.

=== "Code"
    ```lua
    do -- first scope
      local x = 9
      print(x)
    end 

    do -- second scope
      print(x)
    end 
    ``` 
=== "Output"
    ```
    9
    nil
    ```

The local variable declared in first scope is accessible only in first scope and is `nil` for second scope.

# Closing!
Thanks for reading! I hope you enjoyed. We aren't perfect. We make mistakes, typos, etc. so if you found a mistake while reading this article, or any article for that matter, feel free to [report it](https://rodevs-helpers.github.io/Helpers-Documents/Others/Help_Us%21/), and perhaps you can [review us](https://rodevs-helpers.github.io/Helpers-Documents/Others/Help_Us%21/) too! Any feedback is appreciated. 
