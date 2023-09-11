---
title: Saving Game Data..
template: docs.html
comments: true
hide:
  - navigation
---

# Data Stores
**Data Stores** allow you to save data across multiple sessions of your game. For example, if I had a clicker game, I could save the number of clicks someone has for the next time they join my game. Otherwise, their progress would "reset" every time they re-joined the game.

!!! info "Studio Access to API Services"
    When testing a game in Studio, by default it will not be able to access data stores and you will have to go in-game to test. To allow ourselves to test our data stores in Studio;
    1. Navigate to Game Settings via the FILE button, at the top left of Studio. (if "Game Settings" is greyed out, publish your game first or wait a few seconds, some data might be loading.)
    2. Go to the security tab and turn on "Enable Studio Access to API Services"

    ![settingsSceenie](https://imgur.com/PNpqsQN.png)

    Be careful when enabling this setting for live games. The data store used in Studio will be the same one used for the actual game, make sure not to overwrite player data. If you want to be extra safe you can clone your game and use this setting in that test server instead.

## Creating a Data Store
We create a data store by getting the data store service via `game:GetService()` and using the `GetDataStore()` method; which will attempt to get an already existing data store or if one doesn't exist with that name will create a new one.

```lua
local dataStoreService = game:GetService("DataStoreService")
local datastore1 = dataStoreService:GetDataStore("datastore1")
```

## Using a Data Store
!!! warning "You should know:"
    * Local Scripts **cannot** access data stores.
    * Using data stores come with using network calls; these can occasionally fail which is out of your control, use `pcall()` or `xpcall()` to wrap your interaction in case of such an event.
### Setting/Updating and Getting Data
We set data in a data store with the `SetAsync()` method; providing a valid UTF-8 string key, a value to set. In essence, data stores are dictionaries. 

A common practice is to set individual players' data using their UserId as a key (itself or combined with a string, for example `"player_54321"`), and a dictionary containing the relevant data. Here is an example of getting someone's data when they join and print out a message if a "hasPlayed" value is false (in this case, nil, as it will not be set).
```lua
local playerDataStore = dataStoreService:GetDataStore("playerData")
game.Players.PlayerAdded:Connect(function(plr)
    local dataStoreKey = "player_"..plr.UserId 
    local success, playerData = pcall(playerDataStore.GetAsync, playerDataStore, dataStoreKey)
    if not success then
        warn(playerData) 
        --[[kind of misleading, the second value returned by pcall will
        either be the error if it failed OR any value returned by the call
        if it ran successfully.]]
    else
        if not playerData["hasPlayed"] then
            playerData["hasPlayed"] = true
            print("It is " .. plr.Name"'s first time playing!")
        end
        local success, err = pcall(playerDataStore.SetAsync, playerDataStore, dataStoreKey, playerData)
        if not success then
            warn(err)
        end     
    end
end)
```
There are other methods:
* **`IncrementAsync()`**: Increment an integer entry by an integer argument
* **`UpdateAsync()`**: A more complex alternative to `SetAsync()`, takes a key argument and a callback function that takes the current value and DataStoreKeyInfo as parameters and returns the new value. Use this for a safer way of setting data, to make sure data being set by multiple servers at once will not be overwritten. It is slower as it reads before it writes. It also counts toward the [read and write limit](#limits) because of this
* **`RemoveAsync()`**: Takes a key argument and removes the value associated with this key, any `GetAsync()` calls to it will return nil. Returns the value that was removed.

## Limits {#limits}
### Requests
| **Request** |            **Methods which fall under this request**            | **Requests per Minute** |
|:-----------:|:---------------------------------------------------------------:|:-----------------------:|
|     Get     |                           `GetAsync()`                          |  60 + playerCount * 10  |
|     Set     |   `SetAsync()` `IncrementAsync` `UpdateAsync` `RemoveAsync()`   |  60 + playerCount * 10  |
|  Get Sorted |                        `GetSortedAsync()`                       |   5 + playerCount * 2   |
| Get Version |                       `GetVersionAsync()`                       |   5 + playerCount * 2   |
|     List    | `ListDataStoresAsync()` `ListKeysAsync()` `ListVersionsAsync()` |   5 + playerCount * 2   |
|    Remove   |                      `RemoveVersionAsync()`                     |   5 + playerCount * 2   |
Additionally, **Set** requests on the same key will have a **6-second cooldown**

When a limit is reached, requests are put on a queue (respective of their request types; get requests have their own queue separate from set requests) with a limit of 30 requests which will cause your script to error if it is exceeded.

### Storage
|  **Component**  | **Maximum Character Limit** |
|:---------------:|:---------------------------:|
| Data Store Name |        50 characters        |
|     Key Name    |        50 characters        |
|      Scope      |        50 characters        |
|       Data      |     4 million characters    |
To check the length of your non-string data in characters, you can use the `JSONEnconde()` method of [HTTPService](https://www.helpers-documents.ml/Luau-Learning/HttpService/) to convert your Lua data to a serialized JSON table as a string.

## Ordered Data Stores
**Ordered data stores** allow ordered storage (amazing right, I know) of *positive integers **only***. They are useful for something like making a cross-server leaderboard or any other reason you would want to store ordered integer data. We can create one by using `dataStoreService:GetOrderedDataStore()` instead of the regular `dataStoreservice:GetDataStore()` and we can use `GetSortedAsync()` to get our sorted data. `GetSortedAsync()` takes 4 arguments:
1. ascending: boolean
2. pagesize: number
3. minValue: Variant (optional)
4. maxValue: Variant (optional)

You may be wondering; "what is pagesize? pages? I just want my data :pensive:". 
`GetSortedAsync()` returns a DataStorePages object. This one is pretty unique, so I will explain it to you with an example;

```lua
local orderedDataPages = playerAges:GetSortedAsync(true, 10)
--[[here i get my DataStorePages object by using GetSortedAsync on my 
playerAges ordered data store. I pass in true, and 10, defining whether or not
to sort in ascending order and how many values per page. ]]
local page1 = orderedDataPages:GetCurrentPage()
--[[we use :GetCurrentPage to, you guessed it, get the current page in our pages object.
we haven't advanced anything yet so we are of course, on the first page.
now, our current page is an array of dictionaries, which i will explain later on.
for now, i will just print out each page until our "book" is finished.]]
print(page1)
while not orderedDataPages.IsFinished do
    print(orderedDataPages:GetCurrentPage())
end
--[[orderedDataPages.IsFinished is a property of a pages object depicting whether or not
the current page is the last one in the list.]]
```
So, if we take a look at the imaginary output of our script here, we will see something like this:

```lua
{
    {
        key=Player12345,
        value=2134
    },
    {
        key=Player10809,
        value=1506
    },
    {
        key=Player03090,
        value=200
    },
}
```
This looks a bit weird, let me break it down for you. Getting the current page returns an array, containing dictionaries representing the key and value of that item on the page. For example, if the above was our `page1` variable from earlier, if I wanted to know who the number 1 player in my playerAges ordered data store was I would print out `page1[1].key`. This player didn't appear out of nowhere; we still set our data the same way, using `SetAsync()`, only this time it will be ordered for us and we can use this `DataStorePages` object to iterate through our ordered data store, get the top 10 values, or anything else you would expect from an ordered list.

## Versions
Data stores support a handy feature called versioning, which allows you to revert changes made if you are ever in a situation in which that is needed. When you update a data store with `SetAsync()` or `UpdateAsync()`, you aren't actually overwriting any data. Instead, you create new versions of your data which is then used as the base for the next update. There are 3 methods to manage versions.

* `ListVersionsAsync()`
* `GetVersionAsync()`
* `RemoveVersionAsync()`

`ListVersionsAsync()` returns a Pages object, similar to `GetSortedAsync()` of an [ordered data store](#ordered-data-stores). You can use this object to iterate through a list of versions of the key specified in the arguments of the `ListVersionsAsync()` call, with other optional parameters:

2. **sortDirection:** Enum specifying ascending or descending order (Ascending)
3. **minDate:** Date after which the versions should be listed (0)
4. **maxDate:** Date up to which versions should be listed (0)
5. **pageSize:** Maximum number of items to be listed on each page (0) 

Each item in the list will be a DataStoreObjectVersionInfo object. This object has 3 properties:

1. **CreatedTime:** The milliseconds since epoch at the time the version was created.
2. **IsDeleted:** Whether or not the version is marked as deleted.
3. **Version:** Unique identifier for the version, to be used with `GetVersionAsync()` and `RemoveVersionAsync()`

Versions expire after 30 days (apart from the current one, which never expires of course).
Make sure to have a version-management system in place for your game if you ever plan on saving user data properly; being able to revert someone's data back to what it was at a previous date is very important for user support and preventing major data loss.

## Metadata
Keys have metadata associated with them, having two types:
1. **Service-defined metadata:** Default, read-only metadata such as most recent update time and creation time.
2. **User-defined metadata:** Custom metadata set by the user, via the `DataStoreSetOptions` object and its `:SetMetadata()` method.

You manage datastore metadata by expanding your use of the data store methods;
* `:SetAsync()`'s third and fourth arguments, 
  * A table of UserIds to assist with tracking and removal of data associated with content copyright and intellectual property
  * A `DataStoreSetOptions` object in which has metadata that you set via its `:SetMetadata()` method.
* `GlobalDataStore:GetAsync()`, `GlobalDataStore:IncrementAsync()`, and `GlobalDataStore:RemoveAsync()` return a second value (DataStoreKeyInfo object) that contains both service-defined properties and functions to fetch user-defined metadata:
  * `:GetUserIds()`: Fetches the table of UserIds that was passed to SetAsync().
  * `:GetMetadata()`: Fetches user-defined metadata that was passed to GlobalDataStore:SetAsync() through DataStoreSetOptions:SetMetadata().
  * `.Version`: Version of the key.
  * `.CreatedTime`: Time the key was created, formatted as the number of milliseconds since epoch.
  * `.UpdatedTime`: Last time the key was updated, formatted as the number of milliseconds since epoch.
* The callback function of `GlobalDataStore:UpdateAsync()` takes an additional parameter (DataStoreKeyInfo object) that describes the current key state. It returns the modified value, the key’s associated UserIds, and the key’s metadata.

### Limits
|       **Component**       |             **Maximum Character Limit**            |
|:-------------------------:|:--------------------------------------------------:|
|         Key length        |                    50 characters                   |
|        Value length       |                   250 characters                   |
| Entries (Key-Value pairs) | No limit- but the previous limits must be followed |

## Conclusion
That should be all you need to start using data stores to save data across your game's sessions, if you are having trouble with any errors refer to this [error code cheat sheet](https://create.roblox.com/docs/scripting/data/data-stores#error-code-reference) on the Roblox creator documentation.