---
title: Coding With UI
template: docs.html
comments: true
hide:
  - navigation
---

# User Inter Face
UI, commonly known as User Interface is all of the buttons/text you see on your screen. The open shop button, close shop, buy gamepass, etc.
This small tutorial will teach you the basics of UI scripting and in the end.

## Types of UI
The main types of UI that have events you'll want to use are the following:

The [TextButton](https://create.roblox.com/docs/reference/engine/classes/TextButton) is what you'll be using for opening up shops/buying a sword etc.

The [TextLabel](https://create.roblox.com/docs/reference/engine/classes/TextLabel) is what you'll be using to describe how much damage the sword does etc.

The [TextBox](https://create.roblox.com/docs/reference/engine/classes/TextBox) is what you use to type into. This could be used for a boombox, RolePlaying name, etc.

They're of course more you can check out but these are the ones you'll most likely use the most.

## Most Common Mistake While Coding UI
The most common mistake I see is a scripter indexing UI through StarterGUI. Here's an example:

Incorrect way:

```lua
local MyUi = game.StarterGui.OpenShop
```

This is wrong because UI in StarterGui gets **replicated** to the PlayerGui. Meaning any UI in StarterGui will go into a folder called PlayerGui inside of the player.

The correct way:

```lua
local Player = game.Players.LocalPlayer
local PlayerGui = Player.PlayerGui
local MyUi = PlayerGui.OpenShop
```

## The Main Events
Here I'll be showcasing some of the main events that you will use while using UI.

Starting with TextButton we have:

MouseButton1Up
MouseButton1Down

MouseButton1Click

Activated

These events all fire when a TextButton is clicked. MouseButton1Up fires when left clicked is released, 1Down for when it's first clicked, and the same for 1Click.

Activated is also the same but it returns an argument called **InputObject**

I'll be using Activated for demonstration:

```lua
MyUi.Activated:Connect(function()
    print('This TextButton has been clicked')
end)
```

The TextLabel doesn't host any important events, all you'll be doing is most likely changing the text/property of it via script.

Example:

```lua
TextLabel.Text = 'Salzu is now senior helper'
```

Next up, is the TextBox. The only event I ever use for TextBox is **FocusLost**. This triggers when a player clicks off/presses enter on a TextBox.

Example:

```lua
local TextBox = PathToTextBox

TextBox.FocusLost:Connect(function(PressedEnter) -- A true/false value whether they pressed Enter or not
    if PressedEnter then
        print('The user pressed enter')
    end
end)
```

## How To Position/Size UI
As you may know by now, UI is 2d. Meaning it doesn't have a Z value. So we can't use **Vector3.new(X,Y,Z)** or **CFrame.new(X,Y,Z)** for UI.

Instead we use **UDim2.new(X,X,Y,Y)**
Before I explain why it takes X, and Y twice I must explain the difference between Scale and Offset.

Scale uses percentages. So 0.1 would be 10% and 1 would be 100%. This is usually better than offset because it will scale better on mobile devices/other platforms.

Offest uses Pixels, 200 pixels, etc.

Now back to Udim2.new(). It takes X in scale first then X if offset. Same for Y, scale then offset.
You can always just do Udim2.fromScale(X,Y) or Udim2.fromOffset(X,Y)

So in order to size UI, you do UDim2.fromScale(X,y)
Same for position.

### Basic UI Knowledge
All UI, TextButtons, TextBoxes, etc must be parented under a ScreenGui.

A little tip is to parent Local Scripts under the UI so you can do:

```lua
script.Parent.Text = 'NewText'
```

Otherwise, you'll run into the issue of StarterGui/PlayerGui unless you define it directly from PlayerGui.

Many people use true/false for opening UI for example:

```lua
local Frame = script.Parent.Parent.Frame
local Button = script.Parent

local HasOpened = false

Button.Activated:Connect(function()
    if HasOpened then
        HasOpened = false
     else
        HasOpened = true
        Frame.VIsible = true
    end
end)
```

A much, much better way of doing this is to set the visibility to the opposite of the visibility. So if it's true you set it to false, and vice versa.

Example:

```lua
local Frame = script.Parent.Parent.Frame
local Button = script.Parent


Button.Activated:Connect(function()
    Frame.Visible = not Frame.Visible -- If it's true it becomes false vice versa
end)
```

Next up I'll be showing the most common properties you'll use while scripting.

```lua
local Ui = MyUi

Ui.Visible = true/false
Ui.BackgroundColor3 = Color3.fromRGB(R,G,B)
Ui.Text = 'Salzu Is Cool'
Ui.Position = UDim2.new(X,X,Y,Y) -- Scale goes first then Offset
Ui.Size = Udim2.new(X,X,Y,Y)
```

#### How To Tween UI
Unlike parts, you can tween UI with the built-in methods of :TweenPosition and :TweenSize

Example:

```lua
UI:TweenPosition(
    EndPostion, -- UDim2.new(X,Y,X,Y)
    EasingDirection, -- In,Out,InOut
    EasingStyle -- Bounce,Sine,Elastic etc
    Duration
)
```
The same applies to size you just change the EndPosition

## How To Spice Up Your UI
Now that we've gone over the basics of scripting UI we gotta make the UI look good. For this, we'll be using Instances called UICorners and UIStrokes.

These make your UI round and give it a nice stroke around it. They're of course many more in the screenshot below.

![screen1](https://imgur.com/88kpaVU.png)

You can mess around with those, but first, we have to make a button. Insert a ScreenGui and then a TextButton in StarterGui.
It should look something like this

![screen2](https://imgur.com/r0Hp8Ae.png)

Nextly, we're going to change so change the text. Click on TextScaled to make the text bigger. Nextly, we're going to change the font. Multiple fonts are available but my favorite is FredokaOne.

It should look like this:

![screen3](https://imgur.com/JqX8nWZ.png)

Now, we're going to change the text color to white and the background color to blue. This is all my preference you don't have to do this.

We can finally get started on the UI corners and UI Strokes. Insert a UI Corner into the TextButton. We set the corner radius to this **0.1,0**

![screen4](https://imgur.com/N3EkH0P.png)

Next, we have the UI Stroke. At first, it will create a stroke around your text but we can change that via properties.

Change the ApplyStrokeMode to Border, and the thickness to 2.5. The color is up to you.

![screen5](https://imgur.com/yYZqEe5.png)

Finally, I just changed the text and gave it some color and we have this:

![screen6](https://imgur.com/pD1rnwm.png)

This is how I make my UI look good and I hope you learned something from this.

## Closing!
That's pretty much of it. Hope you enjoyed reading it. In case of any mistake, typos, etc. Please report the article. You can also give us reviews [here](https://rodevs-helpers.github.io/Helpers-Documents/Others/Help%20Us%21/)