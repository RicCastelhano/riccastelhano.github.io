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

Our spritesheet has multiple different animations, with different frame ranges and the last two have different starting X positions. So, I created an object with those definitions.

```js
this.animations = {
    idleRight: {
        spriteY: 0,
        frameRate: 14,
        sx: 110.5,
    },
    idleLeft: {
        spriteY: 1,
        frameRate: 14,
        sx: 110.5,
    },
    walkRight: {
        spriteY: 2,
        frameRate: 9,
        sx: 110.5,
    },
    walkLeft: {
        spriteY: 3,
        frameRate: 9,
        sx: 110.5,
    },
    attackRight: {
        spriteY: 4,
        frameRate: 7,
        sx: 110.5,
    },
    attackLeft: {
        spriteY: 5,
        frameRate: 7,
        sx: 110.5,
    },
    dieRight: {
        spriteY: 6,
        frameRate: 11,
        sx: 160,
    },
    dieLeft: {
        spriteY: 7,
        frameRate: 11,
        sx: 160,
    },
};
```
Then the idea is to have a "render window" of the area that we want to present, and we will use the `drawImage()` method from `CanvasRenderingContext2D`.

```js
drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight);
```

That method will need the source image, the source position (x,y) and the source dimensions (width, height). This is the "render window", the area that we will want to display. The following parameters are to declare the actual position on screen that we want it to be render at, and with which dimensions.
So, that's the `s` and the `d` from the parameters, `source` and `destination` precisely.

Consider that we use variables to store the animation status:

```js
this.lastDirection = 'Right';
this.state = 'idle'; 
```

And using that status, we can render the proper sprite:

```js
this.sx = this.animations[this.state+''+this.lastDirection].sx * this.frame;
this.sy = 135 * this.animations[this.state+''+this.lastDirection].spriteY;
this.sWidth = this.animations[this.state+''+this.lastDirection].sx;
this.sHeight = 140
// Destination coordinates
this.dx = this.position.x;
this.dy = this.position.y;
this.dWidth = this.animations[this.state+''+this.lastDirection].sx
this.dHeight = 140;
        
// Draw image
c.drawImage(this.image, this.sx, this.sy, this.sWidth, this.sHeight, this.dx, this.dy, this.dWidth, this.dHeight);
```

Inside the code, you will find more comments explaining how and whys.

Please give it a try, and if you have any questions, I'm here to help.

The final result of this exercise should be similar to this:

![final result](/assets/posts/character-animation-spritesheet/final.gif){: .mx-auto.d-block :}

Here is the [Character Animation using Spritesheets GitHup repo](https://github.com/RicCastelhano/character_animation_using_spritesheet).


Enjoy,

Ricardo Castelhano