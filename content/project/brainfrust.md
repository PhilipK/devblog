+++
title = "Brain Frust"
date = 2020-08-06
[taxonomies]
tags = ["Rust", "WASM","BrainFuck","Interpeter","Compiler"]
[extra]
github="https://github.com/PhilipK/brainfrust"
image="../static/images/brainfrust.png"
description="A small interpeter/compiler for Brainfuck written in Rust"
+++

A small interpeter and compiler for the [Brainfuck](https://en.wikipedia.org/wiki/Brainfuck) (BF) programming language written in Rust.

During a hackathon at my job [Brølstærk](http://broelstaerk.dk/) we had a small challange to write a simple "Add two numbers" program in BF. After that I had the idea to test how good Rust is at writing langauge parsers and interpeters. 
It turns out it was a lot simpler than I expected, so I also made it a compiler, a BF to Rust compiler. It turns out that if you compile a BF ot Rust in the most simple way you can, the programs are still pretty fast because Rust optimises so much.
The project started just being a small CLI program, but I also ported it to WebAssembly (WASM). It was a great experience and fun to remember some of these techniques I had not really used since my UNI days.