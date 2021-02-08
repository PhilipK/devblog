+++
title = "GPU Boids"
date = 2020-06-08
[taxonomies]
tags = ["Unity", "GPU","Compute shaders","Shaders","C#"]
[extra]
github="https://github.com/PhilipK/GpuBoids"
+++

A small simulation of fish in a fish tank.

## Compute Shaders

I have been playing with shaders on and off many times, I love to code something that is visual, and the GPU and its parallelism fascinates me. I wanted to play with compute shaders, because they are shaders that you can use to calculate with, not only for visual things.
They are a little higher level than something like CUDA but low level enough you should be able to use it for most parallel processing.
For this little experiment I used compute shaders to simulate a school of fish.

It was fun to experiment with when it made sense to use the GPU and when to use the CPU.
For the fish, GPU, it was a very parallel problem.
For the sharks, that hunts the fish, CPU, are one or two of the sharks at any time, even if the sharks need to consider every fish the overhead of sending the data to the GPU was just too high.

## Just watch Sebastian

If you want to watch a really great video about Boids you should watch this:

{{ youtube(id="bqtqltqcQhw") }}

His video goes into great details.
