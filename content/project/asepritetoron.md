+++
title = "Aseprite to run"
date = 2020-06-16
[taxonomies]
tags = ["Rust", "Aseprite"]
+++

The first real usable program I made in Rust.

While working on the game Newton i needed a way to quickly convert from an Aseprite export .json file to .ron notation file used by Amethyst game engine.
When I look at the code as i write article (about 6 months later) it is kind of funny to see how far I have come in my understanding of Rust since then. I would definetly have done a lot of things differently now.

This project showed me the value of the small self-contained executalbes that Rust creates. I didn't need a million jars or dlls, just one exe. This started my ideas about "micro executables" that i explain in the Book Mosaic project.
