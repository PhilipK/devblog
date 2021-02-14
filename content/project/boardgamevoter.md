+++
title = "Boardgame Voter"
date = 2015-11-08
[taxonomies]
tags = ["NodeJs", "Socket IO","Websockets","Javascript","Knapsack","ImmutableJS","Redux"]
[extra]
github="https://bitbucket.org/PhilipK/boardgamevoter"
image="../static/images/boardgamevoter.PNG"
description="Vote for boardgames to play"
+++
The idea is that you are sitting with your friends and you really can't figure out what boardgame you to play, and you only have a certain time to play in. So you pull out the "boardgame voter app" and everyone votes on the boardgames they want to play. The app then tries to fit as many games that people really want to play into that timeframe.
Also, if you had multiple game collections peoples would know which games to bring to gamenight.

## Knapsack

The core of this app was the [knapsack algorith](https://en.wikipedia.org/wiki/Knapsack_problem). The weight of a game is its estimated playtime length and its value is the number of vores from players.
The algorithm tries to optimize "value for time", without "breaking up a 2 hour boardgame into 20 mintues".
There are many great implementations out there for knapsack, but it was also fun to implement it myself.

## Socket IO / Websockets

The process would be split into the following steps: create game room, select possible collections, vote for games, show results.
All of this should be orchestrated with a server and multiple clients.
The idea was to use Websockets to do all of this in "real time".

WebSockets where fun and easy to learn and to use, but it quickly became aparent that they where overkill for this little solution. The big difference is to think in Events instead of "request/reply". Also you have to think of the scaleability of a system whenever you introduce websockets. For this case each room would probably be less than 20 people, so no problem.

## Maybe just talk about it instead

This project ended up dying as I realized that it is probably just easier to talk about what you want, and take it as it comes... not everyone is as crazy about picking the "perfect boardgame for the eavening", so i realized that asking friends to go through a 4 step process and filling out a survey to pick a boardgame is maybe a bit much.

In the end, it was a fun project to work on.