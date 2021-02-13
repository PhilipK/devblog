+++
title = "Cardboard Butler V1"
date = 2017-02-16
[taxonomies]
tags = ["React", "ImmutableJS",  "JavaScript", "GraphQL", "JSON", "NodeJs" ,"Azure"]
[extra]
github="https://bitbucket.org/PhilipK/bgg-graphql/"
+++

The first (and no decommisioned) version of Cardboard Butler.

## GraphQL

I had just watched a couple of videos on GraphQL and I was itching to find something to use it for. I had tried to use the BGG API before, but had found it annoying to work with, mainly because it is XML, but also because information is spread out across multiple endpoints.
I used NodeJS to set up a GraphQL server, that would wrap the BGG API. GraphQL was very quick to get started with, but then the problems started showing up:

* The BGG API has a build in backoff, meaning if you make too many requests you will be put on cooldown.
* There was no build in way to limit how deep or big requets users of your GraphQL API could make.
* Everything was in NodeJS and quickly turned into callback hell.

## Caching

To solve the problem of too many requets i set up file caching, storing every request for boardgame information in a seperate file.
I also used GraphQL loaders, that would implement some in mememory caching for each request.
This was almost enough to stop spamming BGG API (i love BGG so i would not want to spam them :-) ).

## Limiting requets

To limit a request in Graph QL you have to change your "simple setup" quite a bit, using continuation tokens and all sorts of things. I never got around to doing this, but if I ever use GraphQL again, I wll definetly think about this earlier while i design the API.

## Immutalbe Data

Immutable data i great to work with! After having used React for a while at this point, I realized the biggest challange was handling "how often and much React rerenders". Enter ImmutableJS a javascript library implementing immutable datastructures, with a consistent easy to use library.
At the time Typescript was not that supported by ImmutableJS, Typescript did not have build in help for immutable data either.
While ImmutableJS was great to work with, I later realized how much I had depended on that one library, so much so that I could not reuse any of my React components without always including ImmutableJS.

## Node JS woes

Look, its nothing personal, I just think that Node JS and are not a good match. I really love languages and systems that are very strict and has lots of help up front. The worst things I know in development are: Runtime Execption (crashes) and Debugging wierd bugs. Most of this projects time was spent trying to figure out "why did it just crash?".
In retrospect I could have eliviated a lot of these problems with better unit testing, but honestly, I think that the language should help you more than that.
