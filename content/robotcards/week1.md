+++
title = "Robotcards: Week 1"
date = 2021-03-14
[taxonomies]
tags = ["Rust", "SDL2","Legion","Aseprite"]
[extra]
image="../static/images/robotcards/week1.PNG"
description="Hello, started"
+++

## Finishing a game

I am going to finish a game. I have always wanted to make a game, and I have started making many, but I have never really finish finished a game.
So here is the goal. By *September 9th 2021*, I am going to release a game, of some size and some way (hoping for a Steam release, but let's see).
I made a bet with my wife that I could do it, so now I really have to do it!

I have 26 weeks!

## What is the game

Right now the game is codenamed "Robot Cards". Because that is what I know, it is about progamming robots, using cards. The gameplay is inspired by some of my favorite games like :

* Roborally (Boardgame)
* Into the Breach
* Hades
* Slay the spire
* Dominion (Boardgame)

The gameplay might change a lot as the weeks go on, but for now the core idea is that you:
You control robots on a board/grid.
Each robot has a set of "registers" that can contain actions they can perform.
You "program" the robots by playing cards on a register.
After the planning the robots will perform the actions one by one.
Robots can push and attack each other.

The game is a rougelike, and deckbuilder, meaning that you get to change the cards you have available after each scenario. If you loose you start over and have to build a new deck (but you can unlock new cards options for your deck).

Also //TODO, i need to work on this elevator pitch.

## The process

The plan is to make a weekly update on what has been made since last week, and to talk about what I will make for the next week.
To anyone reading this (including future me), congratulations you are my accountability partner.

I might make video updates aswell, once I have something that is actually worth showing on video :-)

Each week i will make one of theese post, then plan the next week (I am using Trello for planning). If I during the day get a good idea i add it to a "scratchpad" list in Trello and each week I will then organize and revisit the items.

I will try to do a "sprint planning" each week, to try and keep focus for the week. Also I am trying to keep track of time, since I only have 26 weeks.

I have 3 kids and a dayjob, so I only have about an hour each day to work on this project, maybe if I am lucky a bit more on weekends. Lets say 10 hours a week, that leaves me with 260 hours to make this game.... that is not a lot for a game from scratch. SO I really have to keep focus.

Each week I have to answer two questions:

What is fun about this game? and what is not?

## Tech

I will be making this game in Rust, using SDL2 for input and output and Legion ECS as an ECS library, but besides that the rest will be handmade. I am not using Unity or Unreal, because I want to learn how to do all the steps of the game development process.

## Week 1

This first week, I have gotten started, I have a basic grid, units can move, they can be programmed, you have a deck of cards, a hand and a discard pile. There is currently only one goal for the enemy, and that is to get the goal area. I got A star implemented, so there is a "game", as you can see from the screenshot, there is a long way to go.

## Next Week

During play testing I found that the game was pretty hard, the way I have implemented the player registers, each card has a priorty, that is pretty hard to keep track of. Maybe i will just let each unit have a priority instead, or atleast make it clearer what is going to happen. Next week I will focus on getting the game easier to play, because it is needed to handle  randomness of the cards you are given. 