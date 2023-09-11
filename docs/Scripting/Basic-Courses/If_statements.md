---
title: Introduction To If Statements
template: docs.html
comments: true
hide:
  - navigation
---

# If Statements?

If statements offer you a way to only run a certain piece of code if a certain condition holds true.
They are a very important part of programming.

You might have a door in your game that only players that are level 20 or above should be able to pass, you would use an if statement to check if the player's level is greater than or equal to 20 and only then open it.

## How to use if statements?

Let's look at some examples.
```lua
if true then
	print("It's true!")
end
```
What do you expect to happen? If you guessed that it will print "It's true!", you're right.
If statements always check if the condition between the `if` and the `then` holds true and only then execute the code.

What do you think this piece of code would do?
```lua
if false then
    print("It's true.")
end
```
The correct answer is that it will not print anything. It won't execute `print("It's true.")` because the condition doesn't hold true.

We can also do the same thing with variables:
```lua
local myVariable = true

if myVariable then
    print("It holds true.")
end
```
will also print "It holds true." while 
```lua
local myVariable = false

if myVariable then
    print("It holds true!")
end
```
won't print anything.

**What if we set myVariable to nil?** How does `if nil then` behave?
You can check and you will notice that it behaves just like `if false then`.

### Exercises
1. Create a variable that holds any number and create an if statement that checks if this variable holds true and if so, print "Yes. Numbers are treated like true.".

**The solutions are on the bottom of this tutorial.**

## Operators

There are some operators you can use in the condition to make if statements even more useful.

**`==`** means **equal to**
**`~=`** means **not equal to**
**`>`** means **greater than**
**`<`** means **less than**
**`>=`** means **greater than or equal to**
**`<=`** means **less than or equal to**
**`not`** means **the following condition doesn't hold true**

```lua
if 5 == 5 then
    print("It's true!")
end
```
Will print "It's true" and similarly,
```lua
if 5 * 6 <= 12 then
    print("It's true")
end
```
won't print anything.

```lua
if true == true then
	print("It's true")
end
```
will also print "It's true", since the condition `true == true` will hold true, because `true` is equal to `true`.

### Common mistake
A common mistake that you should avoid is using `=` instead of `==`.
```lua
if true = true then

end
```
will error with the errormessage "`Expected 'then' when parsing if statement, got '='`".

### The operator `not`
`not` basically takes the opposite, so `not false` would be `true` and `not true` would be `false`.
`not nil` would be `true`.


### Exercises:
1. Using an if statement, print "3" if 3 to the power of 10 is greater than 5 to the power of 6.
2. Simplify `not (true == true)`
3. Simplify `not not true`
4. Simplify `not (not (true == false))`

**The solutions are on the bottom of this article.**


## elseif and else

Let's say you want to print "Yes" if a variable holds true and "No" if a variable holds false.
With what we have learned previously, we could do
```lua
local myVariable = true

if myVariable then
    print("Yes")
end

if myVariable == false then
    print("No")
end
```
but there is a better way using `elseif`.
```lua
local myVariable = true

if myVariable then
    print("Yes")
elseif myVariable == false then
    print("No")
end
```
Notice that we do not need an end after the first if statement here, but only at the very end.

### Why is this better than our first code
Well that's because it's more efficient. Let's say myVariable is true, now in our first code, it will perform two checks, first it will check if it's true and print "Yes" and then it will check if it's false.

Now in our second code, it will check if myVariable is true and print "Yes". 
There won't be any further checks, so we turned 2 checks into one check.

But if myVariable was `false`, it would still perform two checks, first checking if it's true and then checking if it's false. We don't really need to check if it's false after we've checked if it's true, because if it's not true then it must be false. This is what `else` does.
```lua
local myVariable = false

if myVariable then
    print("Yes")
else
    print("No")
end
```
will only perform one check.

When we were asked why the code where we used `elseif` or `else` is better than the code where we just straight forwardly used `if`, we said it's more efficient. You should know that the difference in performance between the two in normal use is not noticeable though and we really just do it because of the convention and readability.

### Exercises
1. Check if `7^5` is greater or equal to `5^7`, if it is, print "Yes", if not, print "No" using an **if and an else** statement.
2. Check if `nil` is equal to `false`, if it is, print "Yes", if not, print "No" using an **if and an elseif** statement.

**The solutions are on the bottom of this article.**

## Checking if an object exists

If statements are also often used to check if an object exists.
You can use objects in the condition and they will be treated as `true`. 
```lua
if workspace.Baseplate then
    print("True")
end
```
Would print "True".

But if Baseplate didn't exist, this would error with the errormessage "`Attempt to index nil with Baseplate`".

So how can we safely check if an object exists or not, if we just use `.` like in the example above, it will error if it doesn't? => We can use :FindFirstChild().

### Using FindFirstChild in the condition
FindFirstChild will return the object if it  exists and `nil` if it doesn't. As we know from what we've learned previously, `nil` in the condition will be treated like `false`, so this is a safe way of checking if an object exists or not.

So if we are not sure whether the baseplate exists or not, we could use
```lua
if workspace:FindFirstChild("Baseplate") then
    print("The baseplate exists!")
else
    print("The baseplate doesn't exist!")
end
```

## Logical Operators

Using logical operators, you can often shorten code that uses if statements by a lot.
The two logical operators are `or` and `and`.

### How to use `or`

`condition1 or condition2` checks if either is true (or both).
For example, `false or true` would hold `true`, `true or true` would also hold true, but `false or false` would hold false, since both aren't true.

#### Both are treated as true => selects first
If both of the conditions are treated as true, it will select the first, for example `1 or 2` would be `1`, right away selecting `1` after seeing that it holds true.

#### Both are treated as false => selects last
If both of the conditions are treated as false, it will select the last, for example `nil or false` would be `false` but `false or nil` would be `nil`.

### How to use `and`
`condition1 and condition2` checks if both condition1 and condition2 are true.
For example, `false and true` would be false, `false and false` would be false but `true and true` would be true.

#### Both are treated as true => selects last

If both of the conditions are treated as true, it will select the last, for example `3 and 4` would be `4`.

#### Both are treated as false => selects first

If both of the conditions are treated as false, it will select the first, for example `nil and false` would be `nil`, but `false and nil` would be false.

### Using Logical Operators

Let's say we have a variable and we want to check if it's 3 or 5. Here is how we would do that:
```lua
local myVariable = 3

if myVariable == 3 or myVariable == 5 then
    print("True")
end
```

#### Common mistake
A common mistake is using `if myVariable == 3 or 5` here. While reading this aloud might make it sound fine, it will be the same as just `if myVariable == 3`, as we've learned from "**Both are treated as true => selects first**". 
You need to include `myVariable ==` for each condition to actually make it a check if it's either 3 or 5, like we did above.

### Exercises
1. Simplify `(true and false) or (false and true)`
2. Make a variable that holds "Admin". Then, check if that variable is either "Admin" or "Mod" and if so, print "True."
3. Using logical operators, make a variable hold the number 1 if Baseplate exists in workspace and 2 if not.

**The solutions are on the bottom of this article.**

## Conclusion
Thanks for reading. If you find any mistakes, you can [report them](https://rodevs-helpers.github.io/Helpers-Documents/Others/Help_Us%21/).

## Solutions

### How to use if statements?
1.
	```lua
	local number = 5

	if number then
	    print("Yes. Numbers are treated like true.")
	end
	```

### Operators
2.
	```lua
	if 3^10 > 5^6 then
	    print("3")
	end
	```

3. `not (true == true)` ==> `not true` ==> `false`

4. `not not true` ==> `not false` ==> `true`

5. `not (not (true == false))` = `not (not (false))` = `not (true)` = `false`

### elseif and else
1.
	```lua
	if 7^5 >= 5^7 then
	    print("Yes")
	else
	    print("No")
	end
	```

2.
	```lua
	if nil == false then
	    print("Yes")
	elseif nil ~= false then
	    print("No")
	end
	```

### Logical Operators
1. `(true and false) or (false and true)` ==> `false or false` ==> `false`
2. 
	```lua
	local myVariable = "Admin"

	if myVariable == "Admin" or myVariable == "Mod" then
	    print("True.")
	end
	```
3. 
	```lua
	local myVariable = workspace:FindFirstChild("Baseplate") and 1 or 2
	```
