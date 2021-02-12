+++
title = "Coardboard Butler V2"
date = 2019-08-31
[taxonomies]
tags = ["React", "Typescript", "TDD", "Javascript", "XML", "JSON", "Azure CI/CD" ,"Red Green Refactor","Jest"]
[extra]
github="https://github.com/PhilipK/CardboardButler"
link="https://cardboardbutler.azureedge.net/"
+++

The second (and current) iteration of Cardboard Butler; A webpage to find the boardgame to play with your friends.

## Why do a version 2?

There where multiple reasons that i wanted to re-implement Cardboard Butler;

- After having used many different versions of Redux for React i wanted to see if I really needed a strict framework for a simple site like this
- I wanted to try using Red-Green-Refactor Test Driven Development (TDD)
- I wanted to make a version that did not have use a proxy server for the BGG API
- I realised how deeply dependent on ImmutableJS the code was
- I wanted to set up CI/CD so i didn't have to manully upload files
- I wanted to opensource the project

## Red Green Refactor TDD

I had just seen a talk by Martin Fowler, on Red Green Refactor TDD.
{{ youtube(id="vqEg37e4Mkw") }}

I always try out new techniques and tools on a hobby project before i try to introduce them at work. I knew that Cardboard Butler could be a good project for this, since it would require some testing of async funcitons (fetching data) but also some "complex" behaviour when sorting on multiple critera.

The experience of making a test, seeing it red and then go green was nothing new to me(still feels good). The big difference is that you KNOW that you are going to refactor it after it is green. It is allowed to do the first simple solution that comes to your mind to make it green, even if it is slow and ugly. Once you have made the simple solution you also know that you understand the problem, so your refactored solution is most likely going to be better than if you initially started making the "pretty" version.

This has changed how I approach codeing, even if I don't get to do TDD, i still allow myself to do a ugly version first, just to verify that there is a solution, then I refactor it after. Before i would often spend a long time thinking of the "perfect solution" before i got coding, and then when I actually had done the implementation I realized that the problem was different than I expected.

I 100% recommend trying out "Red Green Refactor TDD" on a project, even if you don't think you are not sure that you will use it later. It teaches you something about how you code, more than just typing on the keyboard.

## Services instead of Redux

Cardboard Butler is not a big, high interaction application, with many moving parts and possible states. It basicly is just a "fetch, filter, sort, render" of an API. Inspired by "Services" from DotNet Core when using Dependency Injection, I tried to seperate concerns into service classes instead of actions and reducers. The pros are that the services are very easy to unit test, also there is no overhead for other developers to understand, you can follow the flow of data by simply "going to implementation". To handle changes i simply used Reacts internal state in a component.
I really liked the simplicity of this solution.
This just goes to show that there are no silver bullets, pick the right tool for the job, don't do overkill.

## No server needed

BGG has an XML api, I wanted to get it into JSON instead.
In the old version, I had made a server to proxy and cache the calls to BGG using GraphQL. While it was a good learning experience, it was also overkill, and the server was costing money to host.

I found an NPM package that transforms XML into JSON [xml-js](https://www.npmjs.com/package/xml-js). The resulting JSON is not quite what you would expect from a normal JSON api (you can tell it used to be xml), but it does the job. I created typescript definitions that matched the output and hid the XML convertion in the service. It worked out great, and I would repeat this any time I have to work with an XML service from a frontend (or maybe even in a backend).

## Using typescript immutable instead of a library

Immutable data structures are great! Specially when working with React and you combine it with Pure Components.
[ImmutableJS](https://immutable-js.github.io/immutable-js/) did its job for the first versions of Cardboard Butler, but, the problem was that I had coded the old version to be deeply dependent on it, even deep down in the render functions of the components. This made porting any component almost impossible. Typescript have gotten some great features for handling [immutable data](https://medium.com/jspoint/typescript-data-immutability-71dc3e604426) that where not arround when I first used ImmutableJS. I don't think that I will use ImmutableJS again, I will just rely on typescript instead.

## CI/CD in Azure

I found out that I ould host cardboard butler on a simple static site in Azure and it would cost me a fraction of running the big server. So I set up a pipeline to just build and upload my project every time I pushed to the master branch. This proccess is pretty simple now, just take a look at Microsofts documentation [here](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website).

## Why opensource?

The original idea for Cardboard Butler came when another system simmelar system "shut down". Suddenly I didn't have a great tool for selecting which boardgames to play, so I wanted to make sure that even if something should happen to cardboard butler, others should be able to maintain it. Also I have used a lot of open-source software, it was time to give something back.

## End result

In the end I think that the rewrite of Cardboard Butler was totally worth it. It has been a great learning experience... but... had this not been a hobby project, then the time spend on rewriting probably whould not have been worth it. Yes the new version better in every way? Yes! But users most likely did not see that anything changed. That is a lot of hours spend on something that does the same thing, without any real new features. The old system worked fine, and the cost of that one server was not really a problem. But, this is not a big coorperate project, so I think it was worth it.
