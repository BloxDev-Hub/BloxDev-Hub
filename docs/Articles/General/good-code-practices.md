---
title: Good Code Practices
---

# Clean code for clean work
A couple of months ago I witnessed an offline, test version of Phantom Forces, where they had all their game's logic in one script. While it's most likely not the case for the live version, it did impart me something important that didn't come across my mind before:
> 10000 lines of code is nigh unreadable in one script. Thousands of badly named variables are no bueno too.

Don't do what PF did. Here are some of the practices for writing clean code that is legible and easily modifiable for everyone.

## Practices:

* Use indentation - this helps you differentiate between scopes and weed out missing keywords like `end` or `}`.
* Keep blank lines within your code - separate your main code from the variables.
* Don't spam blank lines - the more you have to scroll, the harder your script gets to work on.
* Follow conventions!
	* Normal variables can be named with *camelCase* (`playerHealth`, `xpMultiplier`).
	* Use *snake_case* (using underscores) if a variable/function name gets too long (`player_total_health`, `array_of_enemies`).
	* Private variables that you don't want anyone to modify with code can be named with *capital case* (`PLAYER_LEVEL`, `ENEMY_TOTAL_HEALTH`).
	* Functions can be named with *PascalCase* (`SpawnEnemy()`, `TeleportTo()`, `RegenHealth()`).
* Use the Format Document tool in the Script Menu! It's a tool that gets slept on so much, but it really helps.
* Most importantly, standardize your code! Take the time to make your code look all the same for everyone. Use stylesheets or template scripts too if you want.

One of the things I like doing is use `do end` blocks. I come from C#, and it has directives like `#region` and `#endregion` to create code segments that I can collapse to hide away certain chunks of code. You can emulate that using Lua's `do end` statements. While it can affect variable scope if you use one within the `do end` block (though even this can mean good things), it otherwise has no noticeable penalty.

```lua
do
	local name = "valk"
    print(name .. " is cool.")
end

-- print(name)    name does not exist due to scope, so this errors.

-- Output:
-- valk is cool.
```

## Closing
not done yet!!!!!!!!

Have a suggestion to improve this article? Ping me on Discord! @valkyria#0001