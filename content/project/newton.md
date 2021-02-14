+++
title = "Newton Game"
date = 2020-07-13
[taxonomies]
tags = ["Amethyst", "Rust","Aseprite","Specs"]
[extra]
github="https://github.com/PhilipK/Newton"
image="../static/images/newton.png"
description="A spaceship game written in Rust using the Amethyst engine"
+++

This was my first game written in Rust, and the first game I have actually finished.
You play as a spaceship that has to reach a goal before time runs out, without hitting other objects. The kicker is that there is only gravity near big objects, so you have to deal with not flying "too fast" and overshooting your target.

## A game in Rust

I hat watched this video:

{{youtube(id="aKLntZcp27M")}}

And the idea of ECS really inspired me, I also thought that a game was a good project for learning some more Rust.

## Amethyst

Amethyst is a game engine for Rust, and it seemed to be one of the more stable ones out there. The docs are nice and you can get started quickly. But i quickly faced the same problem I always face with Unity, I had to spend more time figuring out how to use the engine than actually programming the game itself. Also, Amethyst did at the time not support mobile targets, and I thought that if I had to learn an engine it should probably support phones.
I decided to test the waters with Amethyst and then move on to something else later.

## Finishing a game

I had set a goal for myself that I needed a playable games, including a titlescreen, gameplay, scoreboard, music and sound. In the end i got all those things to work, but I must admit that I underestimated how long it takes to get all the "not real gameplay" code done.
