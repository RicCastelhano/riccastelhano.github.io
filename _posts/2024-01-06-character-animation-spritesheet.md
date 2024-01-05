---
layout: post
title: Character Animation using a Spritesheet
subtitle: Basic character animation with multiple actions and directions using JavaScript
cover-img: /assets/posts/character-animation-spritesheet/character-animation-spritesheet.png
thumbnail-img: /assets/posts/character-animation-spritesheet/character-animation-spritesheet.png
share-img: /assets/posts/character-animation-spritesheet/character-animation-spritesheet.png
tags: [gamedevelopment, creativeprogramming, javascript]
author: Ricardo Castelhano
---

There are multiple ways to create a character animation for a game. 

One of those ways is to leverage a single file with all the actions and permutations that that character may have. 

One of the specificities of this technique is that it will be better for network performance, instead of a continuous ping-pong request loop for additional images.

**How does it work?**

First we need to have a single file with all the sprites.

For this exercise I'm using free tiles from [GameArt2D](https://www.gameart2d.com/freebies.html).

![game2D](/assets/posts/character-animation-spritesheet/game2D.png){: .mx-auto.d-block :}

That I assembled in a single spritesheet file.

![spritesheet assemble](/assets/posts/character-animation-spritesheet/spritesheet-assemble.png){: .mx-auto.d-block :}

Then the idea is to have a "render window" of the area that we want to present, and we will use the `drawImage()` method from `CanvasRenderingContext2D`.

>`drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight);`

That method will need the source image, the source position (x,y) and the source dimensions (width, height). This is the "render window", the area that we will want to display. The following parameters are to declare the actual position on screen that we want it to be render at, and with which dimensions.
So, that's the `s` and the `d` from the parameters, `source` and `destination` precisely.

Inside the code, you will find comments explaining how to keep track of the direction and actions inside the spritesheet, but tl:dr, we use the sprite dimensions:

``````
Action 1 Animation

first sprite:
x = 0 * sprite.width
y = 0

second sprite:
x = 1 * sprite.width
y = 0

third sprite:
x = 2 * sprite.width
y = 0
``````

We will use the same technique to change actions and directions:

`````
Action 2 Animation

first sprite:
x = 0 * sprite.width
y = 1 * sprite.height

second sprite:
x = 1 * sprite.width
y = 1 * sprite.height

third sprite:
x = 2 * sprite.width
y = 1 * sprite.height
`````

And another different action:

`````
Action 2 Animation

first sprite:
x = 0 * sprite.width
y = 2 * sprite.height

second sprite:
x = 1 * sprite.width
y = 2 * sprite.height

third sprite:
x = 2 * sprite.width
y = 2 * sprite.height
`````

Please give it a try, and if you have any questions, I'm here to help.

Here is the [Character Animation using Spritesheets GitHup repo](https://github.com/RicCastelhano/character_animation_using_spritesheet).


Enjoy,

Ricardo Castelhano