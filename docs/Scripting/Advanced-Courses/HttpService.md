---
title: HttpService
comments: true
hide:
  - navigationtemplate: docs.html
---

# Introduction

This article will teach you the fundamentals of the `HttpService`. At the end of this article, you will know what HttpService is, what it is used for and how to use it.

## What is HttpService?

HttpService is a built-in API Service, allowing developers to send [Http requests](https://www.w3schools.com/whatis/whatis_http.asp) to web servers other than Roblox. Basically, it helps you interact with the internet outside Roblox.

## What can HttpService used for?

As mentioned above, HttpService can help you do basic communications between your Roblox game/experience and off-site web services. Some of those being:

* Data storage (though can be done with DataStoreService)
* Error reporting
* Feedback system
* Real-time communication
* Other fun API stuff

### What **can't** be HttpService used for?
* Interact with [internal Roblox APIs](https://roblox.fandom.com/wiki/List_of_web_APIs) or any Roblox websites.
* Interact with services that are blocked by Roblox.
* Create/host a web server
    * Hence, this service can not respond to any HTTP requests.
* URL embedding (e.g. use an image URL as an UI element, or play a YouTube URL).


Next, you will learn how to use HttpService.

---
## How does it work?

Yes, you will need to know how it works before you actually use it.
Imagine 2 people, "Steve" and "Alex" respectively, communicating with each other. Steve wanted to know how Alex is doing, so he decided to ask her. Now Steve can just come to Alex and ask her how her day's going, but she is away from her home right now. Steve decided to text Alex instead, then after a while, he received a text from Alex, saying that she is visiting her grandma and will return tomorrow.

In this story, Steve is communicating with Alex through texting. Steve sent a question, wanting to know where Alex was and Alex responded with her being at her grandpa's house and she would return by tomorrow.

HttpService works the same way. HttpService communicate with outer servers using the [JSON format](https://www.w3schools.com/whatis/whatis_json.asp) (not regular text!). In order to get information from server X, HttpService send a HTTP request to request data from X (through a method which we will cover in the next part). X will then respond with a data (also in JSON format) that satisfy the required information from HttpService.

??? question "What does JSON looks like?"

    JSON is simply a list of key-value pairs. The key is a string in "" and the value can be in number, boolean, array, list, etc.Each pairs is seperated with a comma. JSON data can be stored in a file with `.json` extension, and can be opened with a web browser like Chrome or Firefox. Most web server communications are done through JSON format.
    ```json
	{
	    "key": "value",
	    "number": 2,
	    "array": [
	        {"value1": true},
	        {"value2": 2}
	    ],
	    "list": {
	        {"list_a": "comg"}
	    }
	    "null": null
	}
	```
---
## How do I use the HttpService?

### Step 0: Enabling the service
HttpService is **off by default.** To start playing around, you will need to turn it on. There are 2 ways to do so:

1. Go to **Game Settings** -> **Security** -> Turn on **Allow HTTP Requests** -> Click **Save**
![placeholder](https://i.imgur.com/C9X3TEY.png)
2. Within the **Command Bar**, run the following command:
```lua
game:GetService("HttpService").HttpEnabled = true
```
![placeholder](https://i.imgur.com/jSFZfP1.png)

!!! attention "Note"

    When your game has yet to be published, the second method is the only option. To turn the service off, simply change from true to false, then run the command again.
    
    Enabling the service won't heavily damage the in-game security, but make sure to have anti-exploit methods for your game!
    
### Then we start coding
It's best to explain with an example. In this article, we will try to get the amount of online players within the [Hypixel Minecraft Server](https://hypixel.net/). This should be interesting enough.

You will use these 2 methods in this example:

* `HttpService:GetAsync(url, nocache, headers)`
* `HttpService:JSONDecode(input)`

Let's do some communication, like Steve and Alex.

### 1. `GetAsync`
In order to know how many players there are in Hypixel, we will request data from that server.

`GetAsync` performs a "Get" request (commonly written as GET) to the target server and get the target information. You can understand "Async" as "waiting", because we don't know when the server will respond. It could be instantly, or 1 second, sometimes 10 seconds. `GetAsync` will yield the script until a respond is given.

#### 1.1. Indicating the target URL
`GetAsync` consists of 3 parameters. We will only use the first one, the `url` endpoint parameter.

Now, we need to determine the endpoint URL.  **An endpoint URL is basically where the information is shown**, and in this example I will use the following URL:
* [`https://api.mcsrvstat.us/2/mc.hypixel.net`](https://api.mcsrvstat.us/2/mc.hypixel.net)

#### 1.2. Find the information
When you open the URL, you will see a very long and confusing text (unless you're using Firefox, they have a very nice viewer for JSON). This is the JSON that is containing information regarding Hypixel.

![raw](https://i.imgur.com/NKq4Loh.png)


Now, our initial goal is to **find the amount of online players**. You might have a hard time finding it so I'll do the hard job for you (just this once alright).

![info](https://i.imgur.com/eVGv4f8.png)

!!! attention "Attention"

    This line indicates that there are, as of the time this image is taken, 40737 online players. **Keep in mind that this number is NOT constant because players join and leave every moment.** These kind of results are expected to change all the time.

#### 1.3. Coding
Now we know where is the information to get, time to open Roblox Studio.

HttpService requests should always be handled within a `Script` under `ServerScriptService`. Create one by **right clicking the "ServerScriptService" -> Insert Object... -> Script**. Name the script however you want!

![script](https://i.imgur.com/TnNEjvW.png)


Now, take a close look at the following script. Each comment will help you understand each line of code.

=== "Code"
	```lua
	-- Get the HttpService through the GetService() method
	local HttpService = game:GetService("HttpService")
	
	-- Declare the target URL
	-- URL must be put inside quotes. If there're quotes within the URL, use \ to escape it
	local URL = "https://api.mcsrvstat.us/2/mc.hypixel.net"
	
	-- As mentioned, GetAsync will return the information so we have to put it into a variable
	local info = HttpService:GetAsync(URL)
	
	-- Print the information into the Output window
	-- If you can't see the Output, go to View -> Output
	print(info)
	```
=== "Output"
	```json
	{"ip":"172.65.230.166","port":25565,"debug":{"ping":true,"query":false,"srv":false,"querymismatch":false,"ipinsrv":false,"cnameinsrv":false,"animatedmotd":false,"cachetime":1657866731,"apiversion":2},"motd":{"raw":["                \u00a7aHypixel Network \u00a7c[1.8-1.19]","  \u00a76\u00a7lSUMMER EVENT \u00a77- \u00a7e\u00a7lLEVEL UP, NEW COSMETICS"],"clean":["                Hypixel Network [1.8-1.19]","  SUMMER EVENT - LEVEL UP, NEW COSMETICS"],"html":["                <span style=\"color: #55FF55\">Hypixel Network <\/span><span style=\"color: #FF5555\">[1.8-1.19]<\/span>","  <span style=\"color: #FFAA00\"><span style=\"font-weight: bold;\">SUMMER EVENT <\/span><\/span><span style=\"color: #AAAAAA\">- <\/span><span style=\"color: #FFFF55\"><span style=\"font-weight: bold;\">LEVEL UP, NEW COSMETICS<\/span><\/span>"]},"players":{"online":39948,"max":200000}, .....
	```
Now the output will look the same as the JSON screen when we open the URL. **But we haven't done yet.**

### 2. `JSONDecode`
Luau (the programming language that Roblox uses) by itself can NOT handle JSON format. The output you're looking at is a string version of the raw JSON data, and it is a nightmare to work with. Thankfully though, HttpService has another method that can help us turning a JSON mess into something we can code with, the `JSONDecode` method.

!!! info "Note"

    JSONDecode can be used whether or not the HttpService is enabled.

So far, our code look like this (without the comments):

```lua
local HttpService = game:GetService("HttpService")
local URL = "https://api.mcsrvstat.us/2/mc.hypixel.net"

local info = HttpService:GetAsync(URL) -- Raw JSON
print(info)
```

`info` right now is a string version of the raw JSON information. `JSONDecode` will turn it into a [`dictionary`](https://create.roblox.com/docs/education/coding-5/intro-to-dictionaries).

`JSONDecode` has only one parameter, the raw JSON respond returned by `GetAsync`.

??? question "Wait, why dictionary?"
	JSON and Luau's dictionary share the same key-value pairs behavior, so the engine can easily "decode" it. After decoding, we can start indexing the information like how we did normally.
- JSON
```json
{
    "key": "value"
}
```
- Luau
```lua
local dict = {
    key = "value"   -- or ["key"] = "value"
}
print(dict.key) --> value
```
The method is simple:

=== "Script"
	```lua
	local HttpService = game:GetService("HttpService")
	local URL = "https://api.mcsrvstat.us/2/mc.hypixel.net"
	
	local info = HttpService:GetAsync(URL) -- Raw JSON
	local info_dict = HttpService:JSONDecode(info) -- Decoded JSON
	
	print(info_dict) -- Print the info
	```
=== "Output"
	**Note: I've cut off some of the output to keep this screen short. Your output will be filled with a alot of bizzare base64 code, but the format will be the same!**
	**Within your output, click the arrow "▶" to expand a table that looks like `{...}`.**
	```lua
	{
    		["debug"] =  ▶ {...},
    		["hostname"] = "mc.hypixel.net",
    		["icon"] = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEAAA......zrDmHEPQgkAAAAASUVORK5CYII=",
		    ["ip"] = "172.65.236.36",
    		["motd"] =  ▶ {...},
    		["online"] = true,
    		["players"] =  ▼  {
    		   ["max"] = 200000,
    		   ["online"] = 39694
    		},
    		["port"] = 25565,
    		["protocol"] = 47,
    		["version"] = "Requires MC 1.8 / 1.19"
	}
	```
Hey look, it's the players information we're looking for! **The amount of players have changed**, but we have talked this through.
![info](https://i.imgur.com/scnPtii.png)

Great, we now have a scriptable data table, all we have to do now is **indexing the data**.
```lua
local HttpService = game:GetService("HttpService")
local URL = "https://api.mcsrvstat.us/2/mc.hypixel.net"

local info = HttpService:GetAsync(URL)
local info_dict = HttpService:JSONDecode(info)

local online_players = info_dict.players.online -- indexing the key
print("There are "..online_players.." players in Hypixel.")
```
Take a look at your output, you will see a line like `There are 32093 players in Hypixel`. Of course, this number is not constant, but if you do see one, that means the request has successfully been done and **you have a basic idea of know how to use `GetAsync` and `JSONDecode`**!

### *. Improvements
While the URL I picked for you is relatively stable and accurate and the Hypixel server is likely never go offline, sometimes **maintenance** or **sudden outage** can occur, and either one of them will be down. This cause 2 problems to appear:
* The endpoint URL is inaccessible, making the HttpService errored.
* The request return an error (caused by the offline Hypixel server), making the HttpService errored.

These are of course not the only problems that might appear during a request. So we will need a proper method to handle such occasions. This is where `pcall()` comes to handy.
`pcall()`, or **p**rotected **call**, is used when a function might fail. `pcall()` return 2 values: `success` and a value returned by the function.
We will protect our request like so:
```lua
local HttpService = game:GetService("HttpService")
local URL = "https://api.mcsrvstat.us/2/mc.hypixel.net"

local success, info = pcall(function()
    local raw_info = HttpService:GetAsync(URL)
    local info_dict = HttpService:JSONDecode(raw_info)

    return info_dict -- the "info" variable will be the "info_dict" we returned.
end)

if success then -- success is a boolean value, it should be self-explanatory.
    local online_players = info_dict.players.online
    print("There are "..online_players.." players in Hypixel.")
else
    warn('Error occurred! '..info) -- This "info" variable will handle our error messages. You can start your debugging process based on this.
end
```

### 3. `PostAsync`
`PostAsync` is a method that "post" data to a specified web server (this is commonly written as "POST requests") and handle results that returned by said server. **However, `PostAsync` can not be replaced by `GetAsync` and vice versa**. This is because some web servers are designated to handle GET or POST requests only.

`PostAsync` has 5 parameters, the first 2 are **mandatory**: 
* The target `url` endpoint.
* The `data` to be sent to the target.

`PostAsync` can be used to make, for example, a feedback system in Roblox, where players send feedback to the feedback section and developers will based on that to improve the game.


### 4. `JSONEncode`
As the name suggest, `JSONEncode` do the exact opposite of what `JSONDecode` do: **convert a dictionary table to a JSON string**. This raw JSON can be used as the `data` argument for the `PostAsync` method.

!!! info "Note"
    JSONEncode can be used whether or not the HttpService is enabled.

`JSONEncode` has only one parameter, a dictionary table.

Here's a quick code example:
=== "Script"
	```lua
	local HttpService = game:GetService("HttpService")

	local info = {
    	feedback = "This game is epic",
    	rate = 9,
    	player = "shogi"
	}

	local json = HttpService:JSONEncode(info) -- Raw JSON in string type
	print(json)
	```
=== "Output"
	```json
	{"feedback":"This game is epic","player":"shogi","rate":9}
	```
	
!!! attention "Note"
    If one of the value in the dictionary is `nil`, that key-value pair **will be ignored.** That means it will not be translated to JSON `null` value.

## Additional links
* [Official Roblox HttpService documentation](https://create.roblox.com/docs/reference/engine/classes/HttpService)
* [More about HTTP Requests](https://www.w3schools.com/tags/ref_httpmethods.asp)
* [More about the JSON format](https://www.json.org/json-en.html)


---
## That's about it
I hope you can use the service to improve your game experience. Good luck bai

---