+++
title = "Robotcards: Week 7"
date = 2021-04-25
[taxonomies]
tags = ["Rust"]
[extra]
image="../static/images/robotcards/week6.PNG"
description="Generic Abilities and Alpha Plans"
+++

## Progress this week

This week I didn't have much time to work on the project (family and work took all my free time), but I did get a few things done.

First I got to plan out everything that is needed for the first "friends shareable alpha". Meaning, I have set a goal that in two weeks, I need to have a playable build, that is finish enough that I can get feedback from a few close friends. 
There are quite a few things that needs fixed before that.

I also got to implement a few more cards and abilities, and I have made the abilities code a lot more generic (so that it is easier to implement abilities).

Currently I am also working on redoing how fonts are rendered. SDL2 font rendering has always been a problem for me, so instead I am redoing by just using a texture generated from a font, that contains one of each character i need. Then I can use the sprite batch to render one character at a time.


## What is fun?

The new cards and abilities show that it is going to be fun.

## What is not fun?

Same as last week: You can still only play one level, and there are no rewards for finising a level.

## Next week

Same as last week: Working on playing more than one level, and getting rewards inbetween.
