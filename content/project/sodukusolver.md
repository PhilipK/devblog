+++
title = "Sodukusolver"
date = 2020-09-10
[taxonomies]
tags = ["Rust"]
+++

A small simple soduku solver written in Rust.

I was thinking it would be fun to make a soduku solver that could give all the solutions to a soduku (in case there where more). There are lots of solutions out there, so I just found one in python and converted it to Rust. 

When I was done, I thought, how about I just give it a empty soduku plate and let it generate all the possible solution there are... i let it run for a couple of minutes and then i got a warning that my harddrive was just about out of space. Turns out there are a lot of possible sodukus (about 10^21) and Rust will gladly let you fill up your harddrive with a text file.