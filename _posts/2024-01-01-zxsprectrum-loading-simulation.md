---
layout: post
title: Sinclair ZX Spectrum 48k Loading Simulation
subtitle: Create a Simulation of a Sinclair ZX Spectrum 48k computer loading the Jetpac game using JavaScript
cover-img: /assets/posts/zxspectrum-loading-sim-post/zxspectrum-load-sim-cover.png
thumbnail-img: /assets/posts/zxspectrum-loading-sim-post/zxspectrum-load-sim-thumb.png
share-img: /assets/posts/zxspectrum-loading-sim-post/zxspectrum-load-sim-cover.png
tags: [gamedevelopment, retrogames, classics, arcade, javascript]
author: Ricardo Castelhano
---

I have been traveling the memory lane for quite some time. And after creating the "breakout" tutorial, I started thinking about other games I have good memories of.

And one game that I definitely want to replicate in JavaScript is [Jetpac](https://en.wikipedia.org/wiki/Jetpac) by [Ultimate Play The Game](https://en.wikipedia.org/wiki/Ultimate_Play_the_Game)

![Jetpac CoverArt](/assets/posts/zxspectrum-loading-sim-post/Jetpac_Coverart.jpg){: .mx-auto.d-block :}

But in the meantime, I found the motivation from Lee Reilly to replicate the entire ZX Spectrum game loading experience.

Loading a game in a ZX Spectrum is an experience all by itself.
The game comes in an audio tape, as shown below.

![Jetpac Tape](/assets/posts/zxspectrum-loading-sim-post/tape.jpeg){: .mx-auto.d-block :}

We connected a tape recorder to the ZX Spectrum computer, typed the command prompt `load ""` and had to wait...and wait...and wait, we did.

I will not go into the intricacies of how the thing works, but I will leave you a link to a post by Richard "[Shred.Zone](https://shred.zone/cilla/index.html)" Körber ([part1](https://shred.zone/cilla/page/440/r-tape-loading-error.html) / [part2](https://shred.zone/cilla/page/441/r-tape-loading-error-part-2.html)) with the steps well explained if you feel compelled to understand those steps.

The loading process is slow, with most of the games taking up to 20 minutes (one entire side of the audio tape). I remember we had some games that took the entire audio - both sides - to load. 

And the process is far from flawless. It is highly prone to errors (again, if you go through those two blogposts by Shred, you will understand why we ended in frustration so often, looking into a screen with the message "R Type loading error."

But geekiness aside, recreating the loading animations is a cool exercise to exercise logic.

I have split the tutorial into multiple steps, and to keep the code easy to follow, each step has its javascript file.

#### Step 0 - Load the ZX Spectrum font file and the Jetpac Game Load Screen
You can freely download and use the [ZX Spectrum Font Family](https://font.download/font/zx-spectrum-7) by Flavie Hammes.

![Step 0](/assets/posts/zxspectrum-loading-sim-post/step0.png){: .mx-auto.d-block :}

#### Step 1 - Lead Signal Animation

The *Lead Signal* has an animation between two colors filling the entire screen: "#007A87", "#720000"

![Step 1](/assets/posts/zxspectrum-loading-sim-post/step1.gif){: .mx-auto.d-block :}

#### Step 2 - Sync Signal Animation

The screen will be divided into thirty horizontal bars, alternating the colors between "#007A87" and "#720000". The bars will be animated with a downward motion.

![Step 2](/assets/posts/zxspectrum-loading-sim-post/step2.gif){: .mx-auto.d-block :}

#### Step 3 - Bitstream Signal Animation

The screen will be divided up into sixty horizontal bars with different heights (originally, it depended on the bitstream data), alternating the colors between "#665B00" and "#001459". Due to the diverse heights, the visual effect seems to be a faster downward motion.

![Step 3](/assets/posts/zxspectrum-loading-sim-post/step3.gif){: .mx-auto.d-block :}

#### Step 4 - Initial Text animation (simulation of writing the command prompt)

![Step 4](/assets/posts/zxspectrum-loading-sim-post/step4.gif){: .mx-auto.d-block :}

#### Step 5 - Game Image Loading Animation

The display of the game screen has a strange behavior. The ZX Spectrum computer was not built with gaming as its primary goal, which may be why it renders the graphics in such a way.

The game area is split into thirds. 

Each third part is divided into seven smaller areas. We will render a line per each of those smaller areas.

After a third is rendered, we jump to the following third until the entire image is drawn.

![Step 5](/assets/posts/zxspectrum-loading-sim-post/step5.gif){: .mx-auto.d-block :}

#### Step 6 - Render the White Game Area During Signals Animation

Throughout the entire loading sequence, the game area is white, waiting for the bitstream to deliver the necessary *data* to render the image.

In this step I just revisited step1, step2, and step3 to allow the correct screen rendering with that white area.

![Step 6](/assets/posts/zxspectrum-loading-sim-post/step6.gif){: .mx-auto.d-block :}

#### Final: Entire Simulation Assembled
In the final step, I add logic to simulate the loading screen from the command prompt until the game throws the mythical "R Type loading error."

![Step Final](/assets/posts/zxspectrum-loading-sim-post/step_final.gif){: .mx-auto.d-block :}

Here is the [Sinclair ZX Spectrum 48k Jetpac Game Loading Screen Simulation GitHub Repo](https://github.com/RicCastelhano/zx-spectrum-loading-simulation).

Enjoy,

Ricardo Castelhano