---
layout: post
title: Tile-Based Game Levels Creation
subtitle: Create Game Levels with Tiles using JavaScript
cover-img: /assets/posts/tilebased-world-post/tilebased-world-cover.png
thumbnail-img: /assets/posts/tilebased-world-post/tilebased-world-thumb.png
share-img: /assets/posts/tilebased-world-post/tilebased-world-cover.png
tags: [gamedevelopment, web, javascript]
author: Ricardo Castelhano
---


There are several ways to build a game world. I created a simple project, a sort of beginners' tutorial, where I focus the attention to a technique called `TileBased`. In summary it will allow us to use `tiles` to generate all the game maps we need.

![Tiles Examples](/assets/posts/tilebased-world-post/tile-example.png){: .mx-auto.d-block :}

We will start to create a bidimensional matrix to define our level visuals. Each empty tile will have the value `0`.

The other numbers corresponds to a specific tile, for instance `1` corresponds to the file `Tile_1.png`.

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

In our `game.js` file, we will start to define the size of each tile, since this is important and will be used heavily on each calculation.

```js
const tileSize = 128;
```

Even the game area sizing is defined using both the variable `tileSize` and the dimensions of the bidimension matrix `levelMap`.

```js
canvas.width = levelMap[0].length * tileSize;
canvas.height = levelMap.length * tileSize;
```

The logic to generate the entire map consists of going through the entire bidimensional matrix `levelMap` and if we find a value different from `0`, we create a new `Sprite` instance (check the `Sprite.js` class to learn how to render the image itself), and keep a reference in a `tileSprites` array. This array will come in handy later on.

```js
const tileSprites = [];
for (let i = 0; i < levelMap.length; i++){
    for (let j = 0; j < levelMap[i].length; j++){
        if(levelMap[i][j] != 0){
            tileSprites.push(
                new Sprite({
                    position: {
                        x: j * tileSize,
                        y: i * tileSize,
                    },
                    imageSrc: './assets/Tiles/Tile_'+levelMap[i][j]+'.png'
                })
            )
        }   
    }
}
```

Inside our game loop we will need to re-render constinuously our game images, but instead of going through the entire `levelMap` matrix, we will use a much smaller array, the `tileSprites`.

```js
tileSprites.forEach((tileSprite) => {
        tileSprite.update()
})
```

My advice goes for a follow through in the entire code. I left multiple comments explaining what the code is doing, and why. And by the end of it, you will have an idea of how to create maps similar to this one:

![Tile](/assets/posts/tilebased-world-post/tilebased-world-cover.png){: .mx-auto.d-block :}


I'm using free tiles from [GameArt2D](https://www.gameart2d.com/freebies.html), and you can download the entire tileset **Graveyard Platformer Tileset** [here](https://www.gameart2d.com/free-graveyard-platformer-tileset.html) (it includes 16 tiles and 14 decorative objects). 

Here is the [TileBased World Tutorial GitHub Repo](https://github.com/RicCastelhano/tilebased-world-tutorial), with proper comments.

Enjoy,

Ricardo Castelhano