+++
title = "Robotcards: Week 3"
date = 2021-03-27
[taxonomies]
tags = ["Rust", "Legion"]
[extra]
image="../static/images/robotcards/week3.PNG"
description="Keeping it simple"
+++

## Progress this week

This has been a productive week. There is not much new visually, but a lot of stuff has happened "behind the scenes"

This week i have finished 16.5 storypoints, last week i finished 9.5 storypoints and week 1 was 13.5. Again it looks like it is somewhere around 10 points pr week, next week i will adjust.

### Tempate based maps

For the battles i need maps. I could try to make a procedual generator, but it would need a lot of finetuning to make fair and interesting maps. So instead I am going with a "Spelunky" map generator. Meaning, i use a template for the map, and then some sub parts of the template are optional.

As a level editor I use a simple pixel editor. I have written a very small program that maps each pixel to a "map tile type", one for empty one for friendly unit, one for enemy and so on. The program then saves a "output.level" file that is just a byte for each map tile, I also store the dimentions of the map. So a 10x10 map will be 102 bytes on disk.

For each level I use Rusts [include_bytes](https://doc.rust-lang.org/std/macro.include_bytes.html) to include the level in the executable.

Now I just need to make a lot of interesting templates, also at some point I will have to add more metadata to each level, like what the goal of the level is.

### A good flow for defining features

My wife got my a A4 notepad and a [Frixion](https://www.amazon.com/Pilot-Retractable-Erasable-Assorted-Disappear/dp/B009QYH644) ball pen that is also erasable. I got a lot of the "bigger plan" for the game sketched out this week. My flow  from feature idea to completion is currently as follows:

* Sketch out the idea on paper untill I have a pretty good idea about how it would work, including if it is possible to implement.
* Create a task for it in the "inbox backlog" in trello, and add a picture of the notepad to the card.
* Try to define how many story points this task is, at this point it is normally not possible, so i have to:
* Define a pretty detailed "todo" list for the task, including "create this component" "make system X" "make a placeholder sprite"
* After defining tasks, the task is usally detailed enough that I have decided the features scope and have a good overview
* Implement the code, step by step following the list

This flow is great for me, because a lot of the tasks do not need access to the code. I have kids, but I might get a great idea when doing the dishes, so I just jot it down on the paper and then I know I can handle it later. It is also great because it is not always that I have enough brain capacity at the end of the day to think "big broad abstract ideas". At those (sleepy) times it is nice to know that "past Philip" has already made an easy to follow list for me (Thanks Past Philip!).

### World stack

A problem I had about the game was how I would switch between menues, and one skirmish and the next and the main menu. Basicly how would I transition from one screen to the next?

I came up with a concept, where instead of operation on one [Legion World](https://docs.rs/legion/0.4.0/legion/struct.World.html) i made a "stack" of game screens. Each game screen contains a world and a [system schedule](https://docs.rs/legion/0.4.0/legion/systems/struct.Schedule.html).
When rendering the stack worlds are rendered bottom up, so if you are in the middle of a game, but you push the ESC button to open the pause menu, a "Pause Screen" is just pushed on top of the current game screen. Since only the top screen gets to execute its systems the screens below are paused, but still rendered.
This makes it very easy to go from one world to another, while maybe still keeping the old screen in memory.

I made a main menu , battle screen, and pause menu so far. The main menu can start a battle by clicking the new game. All it has to do is to push the battle screen on top of the stack (actually it just sets a value "transition resource" and then another system does the hard work).
This should speed up future development a lot.

### Decided on a theme

I have a general idea of the theme of the game now. It is going to be a bit meta.

You program "features" but you have to fight off all the "bugs" untill you make it to the end of the run "Launch Day".
The idea fo the title was by my friend and colleague [@ffMathy](https://twitter.com/ffMathy) so kudus to him.


### Blog/Video every second week instead

Last weeks blog did not really spawn any discussions or give me that much feedback, so I think I will transition to doing a video every second week instead.

## What is fun?

I am happy that I still get stuck just playing the game myself, when I should be doing other stuff.
It is still very rough, but the core loop of the game holds up (for me atleast).

## What is not fun?

I think that i need to start on the overworld, the stuff that connects one skirmish to another. While the single battles are fun, I think I can now (after the refactor) start the work on the overworld.