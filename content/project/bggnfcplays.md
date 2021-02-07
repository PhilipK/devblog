+++
title = "Boardgame NFC Plays"
date = 2017-12-07
[taxonomies]
tags = ["Kotlin", "Android","NFC"]
[extra]
github="https://bitbucket.org/PhilipK/bggnfcplays"
+++
A small app that uses NFC to track which boardgames I play and for how long.

## Purpose of the app

I got a bunch of nfc tags from a friend, and I wanted to try out how to work with them. Also I was playing a lot of boardgames, and I liked to keep track on how much time I played each of them. The idea was that if a game did not get played for a whole year I would have to concider if I should try to sell it.

I thought, "what if I stick an NFC on the inside of each of my boardgames boxes". Then I could put my phone on the game box to start a game timer, and put it on there again (or just push end on the screen) to stop a timer. The app could then push the "play information" to [BGG](https://boardgamegeek.com/), the site I already used to track my games played.
The year was 2017, and I am writing this in 2021, it now seems almost absurd that I got to play so many boardgames with friends that I needed an app to help me track the time, but back in 2017 I guess i did.

## Kotlin

I use Android Phones, and since I was making this just for myself as a Proof Of Concept and to learn about NFC tags, i decided to make it Android native. In 2016 Kotlin hit version 1.0, and it had started to replace Java as the recommended language for Android development.
My first professional job was as a Java developer, I spent about 7 years writing Java, my first app (TaskXP) was in Java, but even after all that I could not be more excited to put Java behind and try Kotlin.

Kotlin did not diasappoint, it instantly seemed familiar and it seemed very lean and clean (unlike the bloat in Java). I would say "If you are ever in situation where you need to do something with the JVM concider Kotlin instead of Java".

## Developing for Android

The whole development process was very pleseant!
The Android development experience has come a LONG way since I made TaskXP. Much better documentation, must easier to understand activies and intents, much better development tools (Android Studio) and it was very easy to get started with NFC tags, both reading and writing to them.

To log the plays on BGG i had to do some login and cookie magic, but even this was easy thanks to the library [OkHttp](https://square.github.io/okhttp/).

## End result

The app worked, and I got it coded in less than a week of sparetime. You would log in with your BGG Credentials, then you would be shown a list of your games. If you click on a game and then hold your phone up to an NFC tag, the app would write the game id on the nfc tag.
If you at any time (even if not in the app) hold up your phone to the NFC tag the app would launch and start a timer.
In short, the app did exactly what it was supposed to!

Do I still use this App? No, I simply don't play enough boardgames that this is a problem for me anymore.
Was it a great learning experience? Yes.
What did I learn? Before this project I would always recommend people to do "cross platform apps", because of how confusing Android development was. Now I learned that it has come a long way, and it might be worth it to do a native app anyways.
