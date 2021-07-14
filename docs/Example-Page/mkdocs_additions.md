---
title: Material for MKDocs additions
---

# Additions

Those are additions provided by Material for MKDocs that will help you make your article look good and fun to read! For more information go to the official site (scroll down)

## Codeblocks

You can highlight codeblocks as if it was discord (pretty ez)

```lua
local function foo(a, b)
	for _ = 1, b do
		a = a * a
	end
	
	return a
end

local n = foo(2, 5)
```

## Abbreviations

You can create abbreviations as you wish, for example:

RoDevs kinda looking VHNCTR

*[VHNCTR]: very hot but not compared to remi

You can also include abbreviations from files with Snippets extension but for that, look up the Material for MKDocs docs.

## Admonition

Admonitions are blocks of text looking kinda hot.

!!! info
    Lorem ipsum dolor sit amet, consectetur
    adipiscing elit. Nulla et euismod nulla.
    Curabitur feugiat, tortor non consequat
    finibus, justo purus auctor massa, nec
    semper lorem quam in massa.
	
!!! warning
    Lorem ipsum dolor sit amet, consectetur
    adipiscing elit. Nulla et euismod nulla.
    Curabitur feugiat, tortor non consequat
    finibus, justo purus auctor massa, nec
    semper lorem quam in massa.
	
For more information about it click [this](https://squidfunk.github.io/mkdocs-material/reference/admonitions).

## Content tabs

You can also add content tabs

=== "ipairs"
	```lua
	local t = {1, 2, 3, 4, 5}
	
	for i, v in ipairs(t) do
		print(i, v)
	end
	```
=== "pairs"
	```lua
	local t = {
		a = 1,
		b = 2,
		c = 3,
		d = 4,
		e = 5
	}
	
	for i, v in pairs(t) do
		print(i, v)
	end
	```
	
## Diagrams

<div class="mermaid">
graph LR
  A[Start] --> B{Error?};
  B -->|Yes| C[Hmm...];
  C --> D[Debug];
  D --> B;
  B ---->|No| E[Yay!];
</div>

[Documentation.](https://mermaid-js.github.io/mermaid/#/)

## Mathjax

$$
\operatorname{ker} f=\{g\in G:f(g)=e_{H}\}{\mbox{.}}
$$

[Documentation.](https://facelessuser.github.io/pymdown-extensions/extensions/arithmatex/)

## Finally

For more information just go [here](https://squidfunk.github.io/mkdocs-material/reference/abbreviations/).