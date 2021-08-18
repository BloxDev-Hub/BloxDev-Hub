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
A couple of months ago I witnessed an offline, test version of Phantom Forces, where they had all their game's logic in one script. While it's most likely not the case for the live version, it did impart me something important that didn't come across my mind before:
> 10000 lines of code is nigh unreadable in one script. Thousands of badly named variables are no bueno too.

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

## Good practices
I wrote another article on practices for writing clean and readable code, under the General section as well. Give that a read!

## Closing
At its core, great code scalability depends on your ability to plan for the future. Expect your game and its code to grow, and prepare your codebase for that. When you have the experience and skill, start thinking long-term for yourself and everyone you might work with.

**A good programmer thinks of solutions for the present; a great programmer also thinks of solutions for the future.**

Have a suggestion to improve this article? Ping me on Discord! @valkyria#0001