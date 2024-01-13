---
layout: post
title: Particle System 101
subtitle: Create a Basic Particle System using JavaScript
cover-img: /assets/posts/particle-system-101/particle-system-cover.png
thumbnail-img: /assets/posts/particle-system-101/particle-system-thumb.png
share-img: /assets/posts/particle-system-101/particle-system-cover.png
tags: [gamedevelopment, creativeprogramming, particlesystems, javascript]
author: Ricardo Castelhano
---

A particle system is a technique in computer graphics used to simulate certain fuzzy phenomena, which are otherwise difficult to reproduce with conventional rendering techniques. Examples of such phenomena include fire, smoke, sparks, or generally any fluid-like entities. 

But, how does a particle systems work?

## 1. Basic Concept:

**Particles:** In a particle system, 'particles' are small, individual graphical objects that represent parts of a whole effect. Each particle can be a simple 2D shape like a dot or a square, or a more complex 3D object.

In this example it will be a simple white circle:

```js
draw(){
        ctx.fillStyle = ctx.fillStyle = `rgba(255, 255, 255, ${this.alpha})`;
        ctx.beginPath();
        ctx.arc(this.x, this.y, 8, 0, Math.PI * 2);
        ctx.fill();
    }
```

**Emitter:** Particles are emitted from a source, known as an 'emitter'. The emitter controls where particles are generated and often their initial direction and speed.

This is our emitter, each `requestAnimationFrame` event will create a new `particle`:

```js
function addParticle(){
    var particle = new Particle();
    particles.push( particle );
}
```

## 2. Properties of Particles:
**Lifespan:** Each particle has a lifespan after which it disappears or 'dies'. This can be a fixed duration or vary randomly within a range.

We will use the `alpha` property to control the lifespan of our particles. When it reaches `0`, the particle dies and should be removed:

```js
for (let i = 0; i < particles.length; i++) {
    let particle = particles[i];
    if (particle.alpha <= 0) {
        particles.splice(i, 1);
    }
}
```

**Behavior:** Particles have behaviors or rules, which dictate their motion and appearance. This can include gravity, wind, or other forces.

In our case, our particles will have a random velocity, in both X and Y axis, and they should move accordingly. We will also reduce the `alpha` property in each iteration:

```js
update(){
    this.x += this.vx;
    this.y += this.vy;
    this.alpha -= 0.01;
    this.draw();
}
```

**Color and Size:** Particles often change color or size over their lifespan, simulating fading or growth.

## 3. Simulation and Animation:
**Physics:** Particle systems often incorporate simple physics to simulate natural movement. For instance, particles might accelerate downwards due to gravity.

**Randomness:** Variability and randomness are key to making the effect seem more natural. This includes variations in speed, direction, size, color, and lifespan.

In our example the randomness is used to determine the horizontal and vertical speeds:

```js
this.vx = Math.random() * 2 - 1;
this.vy = Math.random() * -5 - 1;
```

## Examples in Media and Art:

**Visual Effects in Movies:** Creating explosions, fire, and magical effects.

**Computer Games:** Simulating environmental effects like rain, fog, or explosions.

**Interactive Art:** Particle systems are used in installations where visual effects respond to user interactions or environmental changes.

I will leave you with a basic particle system, code fully commented, for you to twick around and see if you can figure out something cool. There are plenty more to learn in a particle system, but this is a good start.

![Basic Particle System](/assets/posts/particle-system-101/particle-system-cover.png){: .mx-auto.d-block :}

Here is the [Particle System 101 GitHub Repo](https://github.com/RicCastelhano/particle-systems-101).

Enjoy,

Ricardo Castelhano