+++
title = "Robotcards: Week 6"
date = 2021-04-18
[taxonomies]
tags = ["Rust"]
[extra]
image="../static/images/robotcards/week5.PNG"
description="Implementing the mockup"
+++

## Progress this week

This week I have gotten the ui mockup pretty much implemented. This required a bit of rework on how ui sprites where rendered. I found a bug that has been there since the beginning on the game, which ment I had to rewrite a lot of "hardcoded" positions for ui elements. Now the ui can scale with resolution and things are not just pixel hardcoded.

### UI vs UX

One thing I had to change from the mockup, was that I had placed the players cards, and the orbots registers (where you put the cards) on seperate sides of the screen. This ment that you had to move the cards from one of the the screen to the other all the time, this was not good UX. Instead i moved them almost right next to eachother, and then moved the abilities to the right of the screen. This is a classic UI vs UX scenario, because now the screen is a bit "unbalanced" since there is a lot more content on the left than on the right. It is something I will have to fix later.

### Drag and Drop

I also got drag and drop and working now. I made several systems that can work in parallel. One system checks if the mouse is held down on a dragable element. Another moves dragged content to the mouse courser, another checks if a card is dropped on something that can take a "card as input", like a robot registry or a robot ability input.

### Abilities to mitegate randomness

Besides I have also figured out how to do the abilities system.
In the game you use your cards primarrely for programming your units, but to help with the randomness of the card draw, the player can pick some starting "abilities". An ability can take a combination of cards as input, and then performs some kind of action when all the input cards fullfill the criteria.

As an example you can start with an ability that takes two white cards, and turns them into one white card of your choise. This game has input randomness, like games like Slay the Spire and Into the Breach, but besides that, the game is very dependent on context. Getting a "turn left" might be even better than a "attak and deal 10 damage" because it all depends on the current state of the board. Abilities help you mitigate this.

## What is fun?

Abilities already make the game more enjoyable

## What is not fun?

You can still only play one level, and there are no rewards for finising a level.

## Next week

Working on playing more than one level, and getting rewards inbetween.
