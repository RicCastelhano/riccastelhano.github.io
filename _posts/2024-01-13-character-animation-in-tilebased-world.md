---
layout: post
title: NPC Animation in a TileBased World
subtitle: Insert Non-Player Characters in a TileBased World using JavaScript
cover-img: /assets/posts/npc-tilebased-world/npc-tilebased-world.png
thumbnail-img: /assets/posts/npc-tilebased-world/npc-tilebased-world.png
share-img: /assets/posts/npc-tilebased-world/npc-tilebased-world.png
tags: [gamedevelopment, creativeprogramming, javascript]
author: Ricardo Castelhano
---

In a past tutorial I have showed how to create game levels using tiles, in a technique called "TileBased World". I will not explain how this part works here. For reference, please check that particular tutorial. 
Also in a separate tutorial I have shown how to have multiple animations for the same character, using a single image file, called a "Spritesheet". And for that, I also advise to check it, since that animation technique will be skipped in todays tutorial.

In this tutorial the idea is to include Non-Player Characters (NPC) in our game level created with tiles, and to make them move in a safe area.

**How does it work?**

We will have a different matrix with the locations where our NPCs should be placed.

```js
const baddiesMap = [
    [ 0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0],
    [ 0,  1,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  1,  0],
    [ 0,  0,  0,  0,  0,  0,  1,  0,  0,  0,  0,  0,  0,  0],
    [ 0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0],
    [ 0,  0,  0,  0,  0,  0,  0,  0,  1,  0,  0,  0,  0,  0],
    [ 0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  1,  0,  0],
    [ 0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0],
    [ 0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0]
];
```
Then we will create a new JavaScript Class - `Baddie.js`. 
In this class we will import two different spritesheets, since we will have two different baddies. This will be picked randomly.

In the `game.js` file, we will use the same technique used in the game level creation:

```js
/**
 * Create Zombies Baddies
 */
const zombies = [];
for (let i = 0; i < baddiesMap.length; i++){
    for (let j = 0; j < baddiesMap[i].length; j++){
        if(baddiesMap[i][j] != 0){
            zombies.push(
                new Baddie({
                    position: {
                        x: j * tileSize,
                        y: i * tileSize,
                    }
                })
            )
        }   
    }
}
```

Back to the `Baddie.js` class, you will notice that I'm defining a `hitArea` smaller than the sprite image. This will prevent some strange collisions between our NPC and the environment, or even with our future character, when both characters are in fact several pixels apart. So, I define a smaller area around our NPC. I left some code to help in future collision detection debugging:

```js
//hitArea
this.hitArea.x = this.dx+10;
this.hitArea.y = this.dy;
this.hitArea.w = 90;
this.hitArea.h = this.dHeight;
// render the hitArea for debugging purposes
// c.fillRect(this.hitArea.x, this.hitArea.y, this.hitArea.w, this.hitArea.h);
```

Now, we will make our `baddie` to move it's speed amount each `requestAnimationFrame` event. That will make our instances to start moving horizontally on the screen. However, we need to prevent some odd behaviours like walking on the air, our going through the game scenario.

![Image1](/assets/posts/npc-tilebased-world/image1.png){: .mx-auto.d-block :}

We need to create logic to detect collisions between our NPCs and some "invisible" barriers

![Image2](/assets/posts/npc-tilebased-world/image2.png){: .mx-auto.d-block :}

And we will, again, leverage the "TileBased World" technique for that purpose.

```js
const levelMap = [
    [ 9,  9,  9,  9, 13,  0,  0,  0,  0,  0,  0,  0,  0,  0],
    [ 0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0],
    [15, 15, 16,  0,  0,  0,  0,  0,  0,  0,  0,  1,  2,  2],
    [ 0,  0,  0,  0, 14, 15, 15, 16,  0,  0,  0, 12,  9,  9],
    [ 0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0,  0],
    [ 2,  2,  3,  0,  0,  0,  0,  1,  2,  3,  0,  0,  0,  0],
    [ 5,  5,  6,  0,  0,  0,  0,  4,  5, 10, 11,  2,  3,  0],
    [ 5,  5,  6,  0,  1,  2,  7,  8,  5,  5,  5,  5,  6,  0]
];
```

Remember that a value, in that matrix, different from `0` means it is some "physical" tile rendered in our game level. So, in order for our NPCs to move, first they need to be **over** some floor, and to have a `walkable` tile in front of it.

Considering that if we know the (x,y) position of the NPC, we can determine in each tile the NPC is in. So, we will create three different variables to have the current tile, the future tile, and the "floor" tile references:

```js
let tempX1 = Math.floor(this.hitArea.x / tileSize);
let tempX2 = Math.floor((this.hitArea.x + this.hitArea.w) / tileSize);
let tempY = Math.floor(this.hitArea.y / tileSize);
```

We will have three possible moments where our NPC would be colliding or falling from a platform. So, first we check if the current or the next tile's "floor" exists or not

```js
// will the NPC fall ?
levelMap[tempY + 1][tempX1] == 0 ||
levelMap[tempY + 1][tempX2] == 0 ||
```

Then we check if the next horizontal tile is walkable, meaning it does not have any environment tile rendered:
```js
// will the NPC hit a wall ?
levelMap[tempY][tempX2] != 0 || 
levelMap[tempY][tempX1] != 0 || 
```

And the final check is with the game area boundaries, on the left and on the right:

```js
// will the NPC leave the game area ?
this.hitArea.x + this.hitArea.w >= canvas.width ||
this.hitArea.x <= 0
```

If we have a `true` in any of these conditions, our NPC should turn to the other side and keep walking.

As always, I have all the code commented with explanations of what is happening.

Ahhh, do not forget to import the `Baddie.js` class in your `index.html` file:

```html
<script src="./classes/Sprite.js"></script>
<script src="./classes/Baddie.js"></script>
<script src="./maps/level.js"></script>
<script src="game.js"></script>
```

Again, all the tiles that I'm using are free tiles from [GameArt2D](https://www.gameart2d.com/freebies.html).


Please give it a try, and if you have any questions, I'm here to help.

The final result of this exercise should look similar to this:

![final result](/assets/posts/npc-tilebased-world/final.gif){: .mx-auto.d-block :}

Here is the [NPC Animation in a TileBased World GitHup repo](https://github.com/RicCastelhano/NPC-Animation-in-a-Tile-Based-World-Tutorial).


Enjoy,

Ricardo Castelhano