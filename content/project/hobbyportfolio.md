+++
title = "Hobby Portfolio"
date = 2021-02-06
[taxonomies]
tags = ["Static Site Generator","Zola","Markdown"]
[extra]
github="https://github.com/PhilipK/hobbyportfolio"
+++

Using a static site generator to make this webpage, uses [Zola](https://www.getzola.org/)

## The hobby project graveyard 

I think that a lot of programmers have a long list of projects that they have started and never finihsed. I am no exception. But for every project I make I learn something, and I do make cool stuff, even if it is just for me. I realized that instead of "being ashames of not finishing things" I should be happy and proud that I keep learning new things. This page is a tribute to those "fallen heroes/projects". Hopefully readers can learn something from my mistakes, but even if they don't I can atleast look back on my old projects with foundness and pride.

## Static Site Generator

To make this page I looked into a couple of different technologies. I knew that the page needed very little interaction, and mainly was just going to be "blog posts". I had heard of static site generators and looked at what was available. Initially Gatsby looked interesting, but it was maybe a bit overkill, so I looked at alternatives. I heard about [Zola](https://www.getzola.org/) on a podcast and gave it a shot.

## Zola

It does a few things, but it does them very well, and very fast. All I needed was a way to generate html, in a reliable fashion, and Zola does that. Initally I also looked into the Theming, but realized that I need almost no CSS to get something that is good enough. The end result is that I can not generate this whole page in a couple of miliseconds locally to test. For deployment I set up github actions, and for hosting I set up a github page. All in all, completely free hosting and deployment in a couple of seconds.

I am very happy with the result, if you have a small business page or blog I can recommend Zola!