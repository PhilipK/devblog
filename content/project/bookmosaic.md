+++
title = "Book Mosaic"
date = 2020-06-08
[taxonomies]
tags = ["Rust", "C#","Typescript","DotNet Core","Canvas","Rayon","Docker"]
[extra]
github="https://github.com/PhilipK/Rust_mosaic"
image="../static/images/mosaic.png"
description="Generates a mosaic of images and set it as your lockscreen"
+++

Generates a "mosaic" of a collection of images.

## 3 Iterations

This is one of those projects that have been through quite some iterations, I have reimplemented this at least 3 times. So if the listed "tags" at for this project looks a little weird, it is because it is actually 3 projects, at 3 different times, all doing about the same.

## Why make this?

I like to read books, I exclusively read digital books on my Kindle. I try to read a book a week, but that is not always possible, so maybe about 40 books a year. One thing that I realize that I miss is having a book shelf, a place to display my books. I don't want the shelf to show off (look how well read I am) but more to keep the books as memorabilia. Something you walk by, and then, out of the corner of your eye, you glimpse the cover of a great book and then instantly remember all of those great moments from the book.

So the idea was "how about I make a mosaic of all the covers of all the books I have read and put that as the lock screen on my computer"
Also the image should update every time I have finished reading a book (which I track on GoodReads).

## The Algorithm

The Algorithm for this mosaic goes something like this:

- Find out the resolution of the target image
- Decide on a number of columns you want (iteration 1 this was manual, in 2 and 3 it is automatic)
- Resize all images to the with of the column (keeping the aspect ratio)
- Go through each image and add it to the "lowest column", updating the height of the column

This will make an image that looks something like this:
![Mosaic Image](https://raw.githubusercontent.com/PhilipK/hobbyportfolio/main/static/images/mosaic.png)

The trick here is to find the best number of columns, each iteration had a separate way of handling this.

## Iteration 1 - C#, Typescript & Canvas

The first iteration of this was done in a simple typescript webpage. Canvas was used to draw the images. Integration with Goodreads was done through the Goodreads API and some C# code.
The interface was an input field for your Goodreads id, a number input for the number of columns you wanted and a subtmit button to go.

The solution worked.... kind of, I ran into this weird problem with Canvas.
If you are using images from a different origin (a different DNS domain) the canvas will be concidered "unsafe" and you can now not easily download the canvas as an image.
It is possible to get around this with a "no cors proxy" but that just made the whole solution very unreliable. 
Another problem was that the solution was slow, and the whole browser would freeze up for a while when making the image.
But, it worked well enough for awhile.

## Iteration 2 - Docker & DotNet Core

Later I was learning about docker containers, and thought of a rewrite of this project into c# with a library for the image. The plan was to run a docker container on my local machine that would check for new book images, store the images locally and then generate the new mosaic and store it on disk.
I got it working no problem, the c# version was much faster than the javascript one, and getting a dotnet core application running in a container was super simple.
Since this solution was faster and running in the background, i could make a best guess at how many columns where needed, but simply trying columns = n / 2 (where n is the number of pictures) and then iterating backwords (n--) until i had an image where all columns where not full, when i would make the final image with n+1. This worked pretty well, it was ofc slower than just typing the columns myself.

But there where still problems.
I could not really automately set the lockscreen (i couldn't do that in the first solution either), running a whole Hyper VM for just one docker image.
I ended up turning off the container, and just running the program and setting the lockscreen manullly every time i finished a book.

## Iteration 3 - Rust & Rayon

Enter Rust, 2020 (or the later half of 2020 and 2021 so far) has been the year of Rust for me. I wanted to learn about about image proccessing and multi threading in rust.
The new implementation was surprisingly simple compared to both the C# and Javascript version, that might be because it was the 3rd time i was implementing this.
The solution was about 5x faster than the C# version, but the kicker was that now, instead of calculating the number of columns one at a time i could parralize that with Rayon. Instead i could now look at how many wasted pixel i had (pixels from the books not in the final mosaic or pixels not fill out in the final mosaic).
For this solution is just made a CLI, added it to Windows path, and used a little powershell script to run the cli, and then set the windows lockscreen. I triggered the powershell script to run every time i log into the machine.
In the end this solution is the first one that could automate it all... without even spinning up hyper-v vm for docker :-)