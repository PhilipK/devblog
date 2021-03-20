+++
title = "Robotcards: Week 2"
date = 2021-03-20
[taxonomies]
tags = ["Rust", "SDL2","Legion","Aseprite","Testing"]
[extra]
image="../static/images/robotcards/week2.PNG"
description="Keeping it simple"
+++

## Progress this week

This week i have finished 9.5 storypoints, last week i finished 13.5 storypoints. So it looks like my original guess that I will probably be able to finish 10 storypoints every week is just about right.

I think there are two main reasons that i finished less points this week:

- It was my birthday
- I did a lot of things I had not originally planned (sprint scope creep)

Normally bringing new things into a sprint is pretty bad, but this is my hobby project and I decicded that as long as i know I can finish close to the original 10 points a week, I should do what makes me happy or I think is important right now.

### A simplified gamestate for the AI to work on

To make navigation and Enemy planning work, I had to create a simplified world state representation and perfrom my code logic on that state.
Also i had to sync that game state with my ECS, originally I had thought that I could just use the ECS, but queriying the ECS every time i needed to know "if a unit was next to another unit" was slow and a chore to write.

I ended up with a grid resource that keeps the board game state and can perform actions on it.

```Rust
#[derive(Debug, Clone, Serialize, Deserialize)]
pub struct Grid {
    pub height: usize,
    pub width: usize,
    pub content: Vec<GridContent>,
}

pub enum GridContent {
    Blocker(Entity),
    Unit(Entity),
    Enemy(Entity),
    Empty,
}
```

<sup>
Notice the Entity inside the content here, that is the grids only "link" to the ECS, so information about the content in the grid is still stored in the ECS
</sup>

To keep the two systems in check, I perform the changes on the grid, with for example a `perform_move`:

```Rust
   pub fn perform_move(
        &mut self,
        direction: &CardinalDirection,
        from: (usize, usize),
        command_buffer: &mut CommandBuffer,
    ) -> MoveResult {
```

After that I have a Legion ECS system that updates the positions of units based on their value in the grid:

```Rust
#[system]
#[write_component(PositionComp)]
pub fn update_position(world: &mut SubWorld, #[resource] grid: &GridResource) {
    grid.grid
        .content
        .iter()
        .enumerate()
        .for_each(|(index, item)| match item {
            crate::resources::GridContent::Blocker(entity)
            | crate::resources::GridContent::Unit(entity)
            | crate::resources::GridContent::Enemy(entity) => {
                let mut entry = world
                    .entry_mut(*entity)
                    .expect("expeted map entity to have an entry");
                let position = entry
                    .get_component_mut::<PositionComp>()
                    .expect("anything in map should have position");
                let grid_pos = grid.grid.index_to_xy(index);
                position.p = grid.grid_to_world_pos(grid_pos).into();
            }
            crate::resources::GridContent::Empty => {}
        })
}
```

There are many posibilites for performance improvements here, but this is fast enough for me, since we are talking max 100 entities that needs updated.

This split also ment that I realized that i could use TDD for this game to improve my workflow, i wrote a blogpost about it [Here](@/blog/tdd_gamedev_feedback_loop.md).

## Inlining assets

One thing that was just a "fun to do" thing, was inlining assets directly in the game executable. Currently the game sits at 4709 KB, when compressed that is 1513 KB and that is a standalone executable, no dependencies to install first.
It is really fun to me that my game can fit on a floppy disk, if i decide to make a web version the small game size is going to be great for load times.

Inlining the assets was a pretty small rewrite using rusts [include_bytes](https://doc.rust-lang.org/std/macro.include_bytes.html).

## Isometric perspective

I also decided to try out making the game use a isometric perspective after seeing this video:

{{ youtube(id="0fZXlxtMbC0") }}

I really like the result, the one downside is that I can tell that I am going to have to "relearn" how to do pixel art in that perspective. For now everything is just placeholder/debug art. I will have to dedicate some weeks to making the art when I have more of the gameplay narrowed down. There is no reason to make an awesome looking robot if it never gets used.

## Simplifying concepts

This week i tried to simplify the game concepts. Before a unit had registers, and each register held a prioritiezed action (move forward , 3) or (rotate left , 1) then when running the "execute" phase of the game where the robots execute heir programming the next lowest action with the lowest priority score would perform ONE action and then the next and so on and so on. This was pretty confusing and hard to deal with in the planning phase. Instead in week 2, a unit has a priority score, and the unit with the lowest score goes first. A units score is the sum of its cards priorities. This introduces some interesting gameplay "tradeoffs";  play a lot of expensive cards (like attacks) but then go last where the whole world might have changed, or play a few "cheap" cards to make sure you go first?

Another thing was that a units registers would "wrap around", meaning when you finished the last action in the register the next action would be the first in the register. Units also had "points", they could maybe only have 3 registers, but have 5 action points, so the first register would be performed twice. This was also way too complicated to keep track of, and did not really introduce interesting complexity, just noise.
In week 2, the points are removed, and when you reach the end of the register the units turn ends. Next turn you start from register 0 again.

## Game Visibility

This week i got to thinking "what if my game is released and then noone plays it? How would I feel?" to be honest, if no one plays my game, I will still make it, because I really like the experience... but, to be completely honest I want people to play it, because I want to contribute something.
Statistically speaking, there is a pretty good chance that almost noone will play my game. Just last year (2020) there where more thatn 10000 games released [just on Steam](https://www.statista.com/statistics/552623/number-games-released-steam/). My game will be a drop in an ocean, or a (hopefully) shiny penny in a swimmingpool of pennies.

So I thought, what if I write some more about my findings, I can share with the world that way. Maybe I won't make the best game in the world (I will still try), but maybe I can help others make the best game.

Also, I think I might start making small videos (2 minutes or so) about my findings, if nothing else to try it. Besides that I will try to make a blogpost about my findings each week. 

## What is fun?

Currently the enemys only goal is to reach a goal area, and you have to "keep it away".
This is actually surprisingly fun, you have to think of "oh if I push this enemy over here, he will push the other enemy into this area and so on and so on".
I think this game could become really fun.

## What is not fun?

Oh, there is so much that is not fun about this game right now :-)

Today my plan is to try and write it all down and use the whole next week on just experimenting with solutions.

The game board is currenly totally random, meaning that you can end up with a game where the enemy starts on the goal, and you have just lost. To fix this I think i need to work with a "template" map generation, kind of like what spelunky does, as explained in this video:

{{ youtube(id="Uqk5Zf0tw3o") }}

The game only has one goal "stop the enemy" i think i should experiment with more interesting goals aswell.
