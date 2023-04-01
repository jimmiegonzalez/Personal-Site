---
title: ":video_game: Managing Game Zones in Pragma Engine"
layout: post
date: 2022-03-05 22:10
tag: [Pragma Platform, User Guide]
#image: https://sergiokopplin.github.io/indigo/assets/images/jekyll-logo-light-solid.png
headerImage: true
projects: true
hidden: true # don't count this post in blog pagination
description: "This how-to guide was created for students at Thinkful in order to set up and use the API platform tool Postman."
category: project
author: jimmiegonzalez
externalLink: false
---

![Pragma Logo](/assets/images/pragma.png "Pragma Logo")

# Overview

Pragma Engine is a platform that supports cross-platform accounts, game loops, matchmaking, player data, metrics, and more. the engine enables studios to build and operate rich live service games. In this guide, we'll look at managing game zones, a collection of rooms and items in Pragma Engine.

# Understanding Game Zones

In most games when a character enters a new area, the game loads all the newly-adjacent objects, rooms, and items while simultaneously removing the zones that are no longer adjacent. Pragma Engine's game zone management system allows you to add, spawn, and look up rooms and items within any instantiated game zone.

To add and retrieve rooms and items, a world object needs to be created in JavaScript to manage the game zones:

```js
class World {
    constructor() {
        this.roomObjs = {};
        this.items = {};
    }
}
```

Within the world object, `this.roomObjs = {}` generates a list of all rooms, indexed by
zone and room type while `this.items = {}` generates a list of all items, also indexed by
zone and room type.

# Managing Rooms

To generate a list of new rooms, an `addZone` function needs to be created using the `zone` type and `zoneData` as keys:

```js

addZone(zone, zoneData) {

}

```

Within the `addZone` function, we're going to add the following code:

```js

addZone(zone, zoneData) {
    this.roomObjs[zone] = []
    this.items[zone] = []
    zoneData.forEach(roomType => {
        this.roomObjs[zone][roomType.name] = new roomType()
        this.items[zone][roomType.name] = []
    })
}

```

-   `this.roomObjs[zone] = []` generates a list of rooms for this new zone.
-   `this.items[zone] = []` generates a list of items within this new zone.
-   A `forEach` loop then iterates through a list of all included room types while spawning new rooms.
-   `this.roomObjs[zone][roomType.name] = new roomType()` generates a room
    and adds it to the world.
-   `this.items[zone][roomType.name] = []` creates an empty list of items that can be found within the generated room.

We'll then create a second function called `getRoom` that will use the zone and room types as keys to look up the generated room:

```js

getRoom(zone, room) {
    return this.roomObjs[zone][room.name]
}

```

Now that we have our rooms ready to be managed, let's continue by creating a means to manage items.

# Managing Items

To add items in a zone, we'll create an `addItems` function that uses `zone`, `room` type, and `roomItems` as keys:

```js

addItems(zone, room, roomItems) {

}

```

Within the `addItems` function, we're going to add the following code:

```js

addItems(zone, room, roomItems) {
    for (let i = 0; i < roomItems.length; i++) {
        let roomItem = new roomItems[i]()
        this.items[zone][room.name].push(roomItem)
    }
}

```

-   `for (let i = 0; i < roomItems.length; i++)` is a `for` loop that iterates over all the room types.
-   `let roomItem = new roomItems[i]()` is a variable that stores a new item.
-   `this.items[zone][room.name].push(roomItem)` adds the generated item to
    the list for the specified room.

We'll then create a second function called `takeItem` with `itemKey` and `pos` as keys that are going to get all of the items in the current room:

```js

takeItem(itemKey, pos) {
    let roomItems = this.getItems(pos.zone, pos.room)
}

```

We can then add a `for` loop that is going to iterate over each item, and if no item matches, the function will return `null`:

```js

for (let i = 0; i < roomItems.length; i++) {
    if (roomItems[i].keys.includes(itemKey)) {
        let item = roomItems.splice(i, 1);
        return item[0];
    }
}
return null
}

```

-   `if (roomItems[i].keys.includes(itemKey))` is an `if` statement that checks to see if an item can be identified by the provided key.
-   `let item = roomItems.splice(i, 1);` removes the item from the room's item list if it can be identified by the provided key.
-   `return item[0];` returns the item instance.

Last but not least, we're going to create a function called `giveItem` with `item` and `pos` as keys. The `giveItem` function is going to push the item instance into the room's item list:

```js

giveItem(item, pos) {
    this.items[pos.zone][pos.room.name].push(item)
}
}

```

The final code should look something like this:

```js
class World {
    constructor() {
        this.items = {};
    }

    /**
     *
     * @param {string} zone
     * @param {Array<roomtype>} zoneData
     */

    addZone(zone, zoneData) {
        this.roomObjs[zone] = [];
        this.items[zone] = [];
        zoneData.forEach((roomType) => {
            this.roomObjs[zone][roomType.name] = new roomType();
            this.items[zone][roomType.name] = [];
        });
    }

    /**
     *
     * @param {string} zone
     * @param {roomtype} room
     * @returns instantiated room object
     */

    getRoom(zone, room) {
        return this.roomObjs[zone][room.name];
    }

    /**
     *
     * @param {string} zone
     * @param {roomtype} room
     * @param {Array<itemtype>} roomItems
     */

    addItems(zone, room, roomItems) {
        for (let i = 0; i < roomItems.length; i++) {
            let roomItem = new roomItems[i]();
            this.items[zone][room.name].push(roomItem);
        }
    }

    /**
     *
     * @param {string} zone
     * @param {roomtype} room
     * @returns a list of the item instances in this room
     */

    getItems(zone, room) {
        return this.items[zone][room.name];
    }

    /**
     *
     * @param {itemtype} itemKey
     * @param {playerPosition} pos
     * @returns the item if found or null
     */

    takeItem(itemKey, pos) {
        let roomItems = this.getItems(pos.zone, pos.room);
        for (let i = 0; i < roomItems.length; i++) {
            if (roomItems[i].keys.includes(itemKey)) {
                let item = roomItems.splice(i, 1);
                return item[0];
            }
        }
        return null;
    }

    /**
     *
     * @param {item} item
     * @param {playerPosition} pos
     */

    giveItem(item, pos) {
        this.items[pos.zone][pos.room.name].push(item);
    }
}
var world = new World();
```

Congratulations! You've just created a world object that manages rooms and items within a game zone!
