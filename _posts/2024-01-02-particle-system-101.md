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

**Emitter:** Particles are emitted from a source, known as an 'emitter'. The emitter controls where particles are generated and often their initial direction and speed.

## 2. Properties of Particles:
**Lifespan:** Each particle has a lifespan after which it disappears or 'dies'. This can be a fixed duration or vary randomly within a range.

**Behavior:** Particles have behaviors or rules, which dictate their motion and appearance. This can include gravity, wind, or other forces.

**Color and Size:** Particles often change color or size over their lifespan, simulating fading or growth.

## 3. Simulation and Animation:
**Physics:** Particle systems often incorporate simple physics to simulate natural movement. For instance, particles might accelerate downwards due to gravity.

**Randomness:** Variability and randomness are key to making the effect seem more natural. This includes variations in speed, direction, size, color, and lifespan.

## Examples in Media and Art:

**Visual Effects in Movies:** Creating explosions, fire, and magical effects.

**Computer Games:** Simulating environmental effects like rain, fog, or explosions.

**Interactive Art:** Particle systems are used in installations where visual effects respond to user interactions or environmental changes.

I will leave you with a basic particle system, code fully commented, for you to twick around and see if you can figure out something cool.

![Basic Particle System](/assets/posts/particle-system-101/particle-system-cover.png){: .mx-auto.d-block :}

Here is the [Particle System 101 GitHub Repo](https://github.com/RicCastelhano/particle-systems-101).

Enjoy,

Ricardo Castelhano