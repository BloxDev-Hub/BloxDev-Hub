---
title: Client-Server Communication
template: docs.html
comments: true
hide:
  - navigation
---
# Remote Events and Functions
Roblox uses a client-server framework for handling multiplayer games. Roblox engine offers **Remote Events** and **Remote Functions** as a medium for communication between **clients** and **server**.

The device of every player (such as mobile, console, pc) is considered a **client**. In a game, each client is connected to a Roblox computer called **server**. The server plays a major role in game management.
During runtime, any changes made on the server are replicated to clients. 
For example, the position of a base part is changed using a server-side script. As the part changes its position, the server automatically updates every client, and every client changes the position of that part as well. This communication is done by the Roblox engine and developers don't have to care about replication. 

When designing a game, you will find multiple cases where either the server is contacting the client or the client is contacting the server. In such cases, you will have to use **remote events** or **remote functions**. For instance,

* A client wants to move an object.
* The server needs to warn any specific client for violating rules.
* For making in-server announcements.

Communication between client and server can be either uni-directional or bi-directional. For uni-directional communication, we use **remote events** and **remote functions** for bi-directional. 

## Remote Events.
To use remote events, add a remote event in [ReplictedStorage](https://developer.roblox.com/en-us/api-reference/class/ReplicatedStorage).

<img src=https://github.com/Rodevs-Helpers/Helpers-Documents/blob/main/images/remotes1.png?raw=true width="500" height="500"/>

???+ info "Why replicated storage?"
	Remote events and remote functions can only work when both the client and server can access them. [ReplictedStorage](https://developer.roblox.com/en-us/api-reference/class/ReplicatedStorage) serves as a perfect place for remotes. Every object placed in replicated storage is accessible to both the server and clients.

As mentioned earlier, the remote event acts as a single pathway for communication. Here are some possible ways of using remote events.

<div class="mermaid">
graph LR  
   A[Client] --> B{Server};
</div>
<div class="mermaid">
graph LR  
   A{Server} --> B[Client];
</div>
<div class="mermaid">
graph LR  
   A{Server} --> B[All clients];
</div>

### Client to Server
When communicating from a client to the server we call the method **[RemoteEvent:FireServer()](https://developer.roblox.com/en-us/api-reference/function/RemoteEvent/FireServer)**. You can transmit any number of information by passing them as arguments.
Once fired from the client, a remote event can be received on the server by the event **[RemoteEvent.OnServerEvent](https://developer.roblox.com/en-us/api-reference/event/RemoteEvent/OnServerEvent)**. The [function](https://developer.roblox.com/en-us/articles/Function) connected to `OnServerEvent` by default, receives the player who fired the event as the first parameter

Example code:

```lua
-- Script
game.ReplicatedStorage.RemoteEvent.OnServerEvent:Connect(function(player, ...)
print("remote event received on server")
end)

-- Local script
game.ReplicatedStorage.RemoteEvent:FireServer("Eden my beloved")
```

### Server to Client
For server to client communication, we call the method **[RemoteEvent:FireClient()](https://developer.roblox.com/en-us/api-reference/function/RemoteEvent/FireClient)**. The server itself can't determine, to whom you want to fire the remote event. You need to specify that client as the first argument of `:FireClient()`. 
RemoteEvent can be recieved on client by using **[RemoteEvent.OnClientEvent](https://developer.roblox.com/en-us/api-reference/event/RemoteEvent/OnClientEvent)**. 

Example Code:

```lua
-- Local script
game.ReplicatedStorage.RemoteEvent.OnClientEvent:Connect(function(player, ...)
print("remote event received on client")
end)

-- Script
game.ReplicatedStorage.RemoteEvent:FireClient(player,"Eden my beloved") 
```

### Server to all Clients
If you want to fire a remote from the server to all clients, you need to use [RemoteEvent:FireAllClients()](https://developer.roblox.com/en-us/api-reference/function/RemoteEvent/FireAllClients). In this case you are firing remote event to all clients which means you don't need to specify any client.

Code Example:

```lua
-- Local script
game.ReplicatedStorage.RemoteEvent.OnClientEvent:Connect(function(player, ...)
print("remote event received on client")
end)

-- Script
game.ReplicatedStorage.RemoteEvent:FireAllClients("Eden my beloved") 
```

## Remote Functions
As earlier, add a remote function in [ReplicatedStorage](https://developer.roblox.com/en-us/api-reference/class/ReplicatedStorage)

<img src=https://github.com/Rodevs-Helpers/Helpers-Documents/blob/main/images/remotes2.png?raw=true width="500" height="500"/>

Remote functions work similarly to remote events but as a bi-directional pathway.

<div class="mermaid">
graph LR  
   A[Client] --> B{Server};
   B --> C[Client]
</div>
<div class="mermaid">
graph LR  
   A[Server] --> B{Client};
   B --> C[Server]
</div>

The remote function acts as a request and waits for the response and then returns.

## Client to Server
A request can be made from a client to the server by **[RemoteFunction:InvokeServer()](https://developer.roblox.com/en-us/api-reference/function/RemoteFunction/InvokeServer)**. On the server it can be received by binding a [function]() to **[OnServerInvoke](https://developer.roblox.com/en-us/api-reference/callback/RemoteFunction/OnServerInvoke)**. Additional data can also be passed with **[RemoteFunction:InvokeServer()](https://developer.roblox.com/en-us/api-reference/function/RemoteFunction/InvokeServer)** as arguments.

!!! note
	The bounded function will receive [player](https://developer.roblox.com/en-us/api-reference/class/Player) as the first parameter.

Code Example: 

```lua
--script
local function Request_Handler(player, ...)
print("request recived")
return "done!"
end

game.ReplicatedStorage.RemoteFunction.OnServerInvoke = Request_Handler
-- Local script
game.ReplicatedStorage.RemoteFunction:InvokeServer("hi")
```

## Server To Client
!!! error ""
	Request from the server to any client can be made using `:InvokeClient()` and received using `.OnClientInvoke`. However, it is highly recommended not to use it. Making a request from the server to any client can cause the breaking of your game. Because of the following risks

    * If a client got disconnected while being invoked. The invoke call will error.
    * If a client never returned any value, the server will never stop waiting for it.
    * If the client throws an error, the server will pass the error too.

# Limitation
* Any non-string elements of a table passed either using a remote event or remote function will be converted into a string.
* Any instance that exists only on a client will be `nil` on the server.

# Closing!
We hope you enjoyed. Whatever you are learning, please practice it on the spot. Just reading will not help you if you aren't practicing them.
In case of any mistakes, typos, etc please report the article!
