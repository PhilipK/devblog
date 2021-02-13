+++
title = "Aseprite to RON"
date = 2020-06-16
[taxonomies]
tags = ["Rust", "Aseprite"]
[extra]
image="../static/images/toron.png"
description="The first real usable program I made in Rust."
+++

The first real usable program I made in Rust.

While working on the game Newton I needed a way to quickly convert from an Aseprite export .json file to .ron notation file used by Amethyst game engine.
When I look at the code as I write article (about 6 months later) it is kind of funny to see how far I have come in my understanding of Rust since then. I would definitely have done a lot of things differently now.

This project showed me the value of the small self-contained executables that Rust creates. I didn't need a million jars or DLLs, just one exe. This started my ideas about "micro executables" that I explain in the Book Mosaic project.
