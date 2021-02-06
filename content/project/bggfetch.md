+++
title = "BGG Fetch"
date = 2021-02-04
[taxonomies]
tags = ["Rust", "Tokio","Reqwest"]
+++

A 20 lines program that will make a call to [Boardgame Geek API](https://boardgamegeek.com/wiki/page/BGG_XML_API2), parse the output and print out all the urls pictures of boardgames in a users boardgame collections.
This is used together with the cwget project and the imagemosaic program to make a mosaic wallpaper of images from a users boardgames.

The biggest takeaway from this project was how little code you need to do this. If you know the right crates to use, then you can get a lot done by just stiching together a couple of crates.