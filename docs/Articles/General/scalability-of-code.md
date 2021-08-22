---
title: Code Scalability
---

# Disclaimer
This is a fairly long read, but I truly hope what I am talking about here will enlighten you on something.

# Scalability, Development Time & Motivation
**SCALABILITY** is something you won't see Alvinblox or TheDevKing go through because it's "boring" or "irrelevant". I'd argue quite the opposite, and I hope this article will help you see why. 

While there are a couple of definitions to the term:
> *Your code should run well no matter how often it gets used - a dozen or a billion.*

> *Your code should be easy to modify with little to no consequences and difficulty.*

...what I want to focus on in this article is strictly the latter. Far too often I have seen people focus so much on trying to get their code to work in the present that they neglect on future-proofing their code to make it easy for them to modify later.

## Tiredly walking on the last lap
When you work on a game and grow it at some point, your code will most likely span at least a few hundred lines depending on how complicated it is. Once you hit that point, ease of modification of your code starts to become important. 

I have seen scripters storm out the door on even small games, all of them with complaints like:
> *"All the scripts and functions are everywhere!"*

> *"I can't read the code anymore, it's so messy!"*

> *"Why is the code style so bad?!"*

> *"I'm new to this and I don't even understand what this does!"*

> *"I remove this thing, another breaks! How do I work with this piece of junk?!"*

When you start neglecting how to Code For The Future, problems like these arise very quickly, and it gets progressively more difficult to mitigate and fix. 

Let the problem grow enough, and development can sometimes even come to a halt - you won't be getting new content out anymore, rather you'll be spending lots of time fixing existing code and its problems. Frustration grows and patience wears thin as you stop feeling motivated since you aren't pumping out new content, and burnout starts setting in.

So why let these problems arise in the first place?

## Prevention
Here I'll list some of the ways you can adopt in your development to help improve scalability and improve development time across the board. It's non-exhaustive, but here are some of the things we most commonly see.

### Name your variables/folders/scripts properly!
Don't name those aforementioned stuff with names that are vague and not immediately understood by everyone else (and even you after a while).

Names like `e`, `ph`, `scriptstuff`, `trashfolder` should be avoided; name your stuff properly! Do you have a folder of scripts that all handle the datastore aspect of your game? Name the folder something relevant like `Datastore`!

========
### Learn to write clean code!
I wrote another article on practices for writing clean and readable code, under the General section as well. Give that a read!

========
### Don't write all your code in one script!
People have asked me if they should write their code in one script, and I wish the Phantom Forces example I made illustrates my answer:

> A RESOUNDING **NO**.

Plan for the future. If you think you'll need a lot of post-processing related code, even if you only have 6 lines of that at the moment, move it over to a new script and work on that moving forward!

Also for this reason don't bother minifying code (removing all the whitespaces/indents in your code). Sacrificing a massive part of readability for even just a very minor improvement in performance is by no means a good trade!

========
### Use folders!
Folders are for scripts just like how models are for groups of parts. Keep all your related scripts in one properly named folder!

========
### Use module scripts!
Module scripts are your best friends - bring them on board! Haven't learnt them yet? Learn them!

If you have lots of functions/values that are related/aimed towards doing the same thing, separate it from your main script and put it in a new module script.

And again, if you have several module scripts aimed towards a common goal, use folders to organize them too!

**This is also why I do not recommend _G.** `_G.` is not slower than module scripts at all, but if you have too many values in `_G.`, debugging it can be a nightmare. If you need values to be shared across scripts at all, again use module scripts! They are just the same as `_G.` in principle, and are infinitely more readable, modifiable and scalable!

========
### Don't "nest" require statements!
What I mean by this is having a module script `require` another module script, and so on. When you nest it too many times, you create lots of dependencies within your module scripts.

This practice can get problematic - if a base module script that a group of module scripts rely on fails, all of the module scripts within that group fails too. If that group of module scripts fail, another group of module scripts that rely on them also fails, and the chain continues.

You'll have to trace back more, and debugging becomes slower and more tedious. Don't nest `require`s.

I'll explain this more in another article: Loose coupling.

========
### Document your code!
This holds especially true if you're working with teams. 

Don't be afraid to use comments/comment blocks to explain how a certain part of your code works and what it does. Using comments don't make you seem stupider or weaker - in fact, quite the opposite.

This is especially if you have a collection of functions (eg: a library) that you're sharing with multiple people, and they all use it frequently.

Examples include:

```lua
local regenAmount = 100 -- regens player hp by this amount.

-- PrintPlayerNames()
-- Loops through the Players service, then prints out the names of each.
local function PrintPlayerNames()
	for i, v in ipairs(players:GetPlayers()) do
		print(v.Name)
	end
end
```

**Obviously use comments in moderation too.** No one needs to know about what a variable is for if it's something obvious such as `local player = game:GetService("Players")`. Too many comments add noise to your code as well.

## Closing
At its core, great code scalability depends on your ability to plan for the future. Expect your game and its code to grow, and prepare your codebase for that. When you have the experience and skill, start thinking long-term for yourself and everyone you might work with.

> **A good programmer thinks of solutions for the present; a great programmer also thinks of solutions for the future.**

Have a suggestion to improve this article? Ping me on Discord! @valkyria#0001