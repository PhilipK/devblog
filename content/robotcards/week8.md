+++
title = "Robotcards: Week 8"
date = 2021-05-02
[taxonomies]
tags = ["Rust"]
[extra]
image="../static/images/robotcards/week8.PNG"
description="Font Textures, Github Actions and Multiple Decks"
+++

## Progress this week

This week I re-worked how fonts work, made some github actions, a few more cards and abilities and implemented picking a reward after a won battle.

## Font Textures

One thing that had been bugging me for a while was how fonts where handled. The SDL2 rust wrapper had some very "hard to work with" lifetimes that made it hard to keep a font loaded in memrory.
The way I got around this before was to keep track of every text in the game world, and a map of every text that was generated into a texture.
There where a few problems with this:

### The problem

Every time I needed a new font I would have to:

1. serialize the font file to  disk (in a temp folder)
2. load that file into memory through SDL2
3. Generate the texture (with the given color) for that text
4. Save the texture in a hashmap (key was text and font colour)
5. THEN i could render the texture to the screen

While it was not something that was an imediate problem, I was noticing that the memory use of the game would just rise as more and more different text was shown on screen.
And I really didn't like that I had to touch the harddrive so often.

### The solution

I found this little tool online [https://evanw.github.io/font-texture-generator/](https://evanw.github.io/font-texture-generator/).
It lets you generate a texturemap (and a json file that descripbes the position and size of each character) from a font.
I rewrote the renderer (it is now much leaner) and made a new system that looks for anything with a TextSprite components. It then generates a sprite batch (a sprite for each character in the text) from the text and each of those sprites to the batch.

{{ blogimage(path="../static/images/robotcards/texturemap.png")}}

This also means that I can remove the font from assets, and SDL2's font rendering feature.

### The result

The end result is that I now can handle multiple fonts, the renderer is much simpler (it ONLY renders sprites to the screen),  the game uses a lot less memory and the binary is a lot smaller.
{{ blogimage(path="../static/images/robotcards/memoryuse.png")}}
{{ blogimage(path="../static/images/robotcards/binarysize.PNG")}}

## Github Actions

After hearing this talk:
{{ youtube(id="t9HRzE7_2Xc") }}

I looked into how I could start out early with a little devops for my game.
I use github, so I looked into github acitons.
I was very surpriced how easy it was to implement github actions.

Initially I made an Action that would test my unit tests on linux, macos and windows... then I found out that one minute of build time on macos costs you 10 minutes of billable minutes.... So now I have a linux action that runs on push to main branch that runs tests. I also set up scheduled action that builds a windows release and generates a changelog every saturday.

## What is fun?

The game is still fun to play

## What is not fun?

Overworld still does not work and still too few levels.

## Next week

Working more on getting the first playable Alpha
