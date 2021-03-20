+++
title = "Using tests to speed up your feedback loop"
date = 2021-03-19
[taxonomies]
tags = ["Rust", "Legion", "ECS", "Testing","TDD","Red, Green, Refactor"]
[extra]
image="../static/images/blog/ecs_and_testing/cover.PNG"
description="When is it worth unit testing games? How and when do i test? And what can we bring with us into non-game-dev?"
+++


## TL;DR

In my experience, you can speed up your workflow in UI and Game development, by writing tests for the edge/hard-to-reproduce cases.

## TDD

Honestly, I make mistakes all the time, it is part of being human, and when you deal with big interconnected systems it becomes impossible to keep track of everything.
That is why I like being told that I made a mistake as soon as I can. I think that is why I Rust. Rusts speed is great, but even if it wasn't speedy I would use it, because it prevents me from making so many mistakes at compile time. Rust fits my temperment.
There are still mistakes that a compiler can not find for you; for those cases automated tests help.
I like to do Test Driven Development (TDD)! I like to write tests whenever I can, and if I can do them before I do implementation that is even better. You don't have to like tests, but in this post I will show how I use tests not to "slow me down" but to speed up my development flow and feedback loop.

## Backend vs Ui testing

I have a background in "full stack" development, meaning some backend and more frontend. For me it has always been easier to write tests for the backend, a simplified flow for backend code is:

- Set up a state
- Call a function that performs some state change
- Check the state

For UI it is harder, you are always working with a user and a browser, how do you mock that? The "state change flow" becomes complicated by DOM Changes, Rendering and so on. There are many different workarounds, but the problem is always that you have a tight integration the browser which you do not want to test.
Besides that, how much do you test the UI? Should you test that a button is the right shade of green? Maybe/Probably not. Should you verify that the UI sends a request to the server when a button is sent? Probably, but what about that transition from left to right? Or that things are alligned to the left?
Most times it is easier to look at the webpage and "see" that something is off.

## Gamedev

I am currently working on a game build from (almost) scratch (See my weekly devlopment blog [here](@/robotcards/_index.md)), and I am trying to taking my finding from the gamedev world with me into my other other development.
As far as I can tell, TDD is not that wide spread in game development, maybe on online servers, but not that much in the actual game clients.
I got to thinking why this is? I think that it is because, like in UI development, a lot of what makes a game is what makes it "feel good" and that is not something that is easy to describe and test for.

When I started making my own game, I (without thinking about it) started coding without doing any tests. My top priority was to "get going" and then "iterate on the gameplay", I guess I thought "tests will slow me down".
Things where going great, even without tests, a lot of it was just some simple code.

## Testing with a ECS

After a week of development, I wanted to implement a feature in my game, where a robot can damage another robot if it "squishes" it. A tobot gets squisnhed, if it is being pushed by another robot, but is then prevented from moving (because it hits a blocker, like a wall). The complicated part of this is that this can chain, so a robot can push a robot that pushes another and so on and so on.
This was a bit tricky, because setting up this chain of events takes time in the game and if there is a bug have to play to that point of the game again.
I thought to myself "what would I normally do here if it was not a game?", I would make a testcase first, make a simple solution to that test, refactor a bit, and then repeat, until I had covered all the cases I could think of (also know as Red, Green, Refactor).

I use an Entity Component System for my game (there are many great explanations of how they work out there, so give it a google). I started seperated out my logic from the system that would perform the "sqish", then I realized, but do I really have to do this seperation?

For this project I am using the ECS library "Legion", where each system is actually just a function, that takes some input:`

```Rust
pub fn play_actions(
    world: &mut SubWorld,
    command_buffer: &mut CommandBuffer,
    #[resource] play_state: &mut PlayStateResource,
    #[resource] grid: &mut GridResource,
) {
```

The system works on a game world. So I realized that i could tests the whole system, if I could give it a game world, I could run the system and check if it did what I wanted afterwords. The flow became:

- Set up a world
- Call a function that performs some world change
- Check the world

Replace the word "World" with "State" and you have a test flow that looks a lot like the simple-to-test backend test flow.

In legion this is possible, but you will have to use a bit of unsafe code, but honestly, I don't think that is a problem since it is just for testing.

First you can make a test module direcly next to the system definition, because of the cfg this code is only included in the test build, and not in the actual game.

```Rust
#[cfg(test)]
mod tests {
    use super::CardinalDirection;
    use crate::resources::GridContent;
    use crate::resources::*;
    use legion::{world::ComponentAccess, Resources, World};

    use super::*;

    #[test]
    fn play_squish() {...}

```

Inside the test we can then setup exactly the scenario we want to test for:

```Rust
   // Arrange
    let mut world = World::default();
    let mut resources = Resources::default();
    let mut grid = GridResource::new_test();

    let squish_unit = command_buffer.push((Health::new(1, 1), 1));
    ...
    command_buffer.flush(&mut world, &mut resources);
    let mut subworld = unsafe { SubWorld::new_unchecked(&world, ComponentAccess::All, None) };

    ...
    /// Act
    play_actions(
        &mut subworld,
        &mut command_buffer,
        &mut play_state,
        &mut grid,
    );
    command_buffer.flush(&mut world, &mut resources);

    ...

    // Assert
    assert_eq!(
        0,
        world
            .entry(hit_unit)
            .unwrap()
            .get_component::<Health>()
            .unwrap()
            .current_health
    );
```

I have comittet some of the details here (marked with ...) to keep it it easy to read.
When I run `cargo test` this runs in a second or two, and i instantly know if my code work.

I am sure you can do something simelar, without using ECS, but it sure is easy to do when you have one.

## Improving your feedback loop

The point is: we can use tests for more than verifying correctness, we can use test for fast feedback loops.

By using tests for those hard-to-reprocuce/edge cases, you don't have to play to certain a spot in my game, or make a save game that I can load up and verify behavior in. Just run the tests, because the they set up the a world state that would will the behaviour to verify.
In general, remember; The magic is not only in the Act or the Assert, it is also in the Arrange.

There are things that are just better to test by running the game, and you can never unit test if a game is fun, or if a "transition from a to be looks right", but you can verify those edge cases, and you can improve your feedback loop.
If you have to choose, focus on testing the edge cases, instead of the "main flow".
You will quickly realize if something is wrong with the main flow, if nothing happens when you click a button or if an enemy does not take damage.
Finding that the whole page crashes if a server gives an "backoff" or that the third unit that gets "squished" does not take damage, that is where tests can help, in both UI and Gamedev.

## Bringing it back

This brings me back to what we can learn from gamedev about about frontend. Just like in a game, there are things that you just have to look at and get a feel for; don't test those! Instead focus on testing those things that have hard to verify logic and scenarios that don't happen often or are hard to set up.
Not only because you verify correctness, but because you improve your developer feedback loop and save yourself a lot of time clicking around in a UI.
Structuring your UI changes into the state -> action -> state flow helps a lot on testability for both ui and gamedev, but remember to use tests to optimize your workflow, not slow it down.
