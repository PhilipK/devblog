+++
title = "CWget"
date = 2021-01-27
[taxonomies]
tags = ["Rust","Reqwest","Rayon", "Tokio"]
[extra]
image="../static/images/cwget.PNG"
description="A small cli program that takes a list of urls and downloads the content to a target folder"
+++

A small cli program that takes a list of urls and downloads the content to a target folder (but only if they are not already downloaded).

Using both Tokio and Rayon is maybe overkil, but it was fun to see how parralizable you could make downloading files, in the end this project was maybe an hour to make and it was fun to learn.
