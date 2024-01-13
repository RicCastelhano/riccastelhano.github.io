---
layout: post
title: Breakout Game Tutorial
subtitle: Create a Variation of the Classic Game Breakout using JavaScript
cover-img: /assets/posts/breakout-game-post/Breakout-game-cover.png
thumbnail-img: /assets/posts/breakout-game-post/breakout-game-thumb.png
share-img: /assets/posts/breakout-game-post/Breakout-game-cover.png
tags: [gamedevelopment, retrogames, classics, arcade, javascript]
author: Ricardo Castelhano
---


Two years before I was born, **Atari, Inc.** developed and published an arcade videogame called *Breakout*.

![Breakout Example](/assets/posts/breakout-game-post/Breakout_game_screenshot.png){: .mx-auto.d-block :}

 
My dad was a computer programmer back in the days when computers were big enough to fill up an entire living room. And some years after my birth, I do remember that my dad brought home our first computer - a magical *Sinclair ZX Spectrum 48K*. 
 

![Sinclair ZX Spectrum 48k](/assets/posts/breakout-game-post/ZXSpectrum48k.jpg){: .mx-auto.d-block :}

I was a kid somewhere between the ages of 6 and 8. And it was magical to have access to a computer so small yet so "powerful" that allowed us to play all those great games (don't judge; in my kid's mind, it was magical indeed).

Since my dad's passing, I'm recalling more and more late memories.

In 1987, **Imagine Software Ltd** released a new version of that game, specifically for Spectrum computers - it was called *Arkanoid*

![Arkanoid](/assets/posts/breakout-game-post/Arkanoid.jpg){: .mx-auto.d-block :}

And I did spend hours playing this game with my dad.

In a good hommage to those days, I created a short tutorial on how to build a similar game.

![BreakoutJS](/assets/posts/breakout-game-post/breakout-game-thumb.png){: .mx-auto.d-block :}


We will go through how a game loop works:

```js
// Game Loop
function animate(){
    window.requestAnimationFrame(animate);
    (...)
}
animate();
```

How to control the `paddle` using the keyboard:

```js

function keyboardController(){
    
    paddle.velocity = 0;

    if(keys.a.pressed) paddle.velocity = -1 * paddleSpeed;
    else if(keys.d.pressed) paddle.velocity = paddleSpeed;
}

window.addEventListener('keydown', (event) => {
    switch (event.key) {
      case 'd':
        keys.d.pressed = true;
        break
      case 'a':
        keys.a.pressed = true;
        break
    }
});

window.addEventListener('keyup', (event) => {
    switch (event.key) {
        case 'd':
          keys.d.pressed = false;
          break
        case 'a':
          keys.a.pressed = false;
          break
      }
});
```

And how to detect collisions between our `ball` and the game area:

```js
function wallCollisionDetection(){
    (...)
}
```

Between the `ball` and each `brick`:

```js
function brickCollisionDetection(){
    (...)
}
```

And between the `ball` and our `paddle`:

```js
function paddleCollisionDetection(){
    (...)
}
```

I left the code fully commented with explanations of what the code is doing and why. so, if you go through the code (and all the comments), you will know how the *Breakout/Arkanoid* game works by the end of it.

Here is the [Breakout Game Tutorial GitHub Repo](https://github.com/RicCastelhano/breakout-game-tutorial).

Enjoy,

Ricardo Castelhano