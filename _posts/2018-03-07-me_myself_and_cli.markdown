---
layout: post
title:      "Me, myself and CLI"
date:       2018-03-07 20:42:13 -0500
permalink:  me_myself_and_cli
---


Developing a CLI project from scratch for the first time is not an easy task, just because you don't know where to start.
Still, the videos provided by Flatiron + previous lectures and labs + info on the web makes it doable.
If I did it - anyone can do it :-)

I started with reviewing peer students' code ("Seems pretty organized", I thought), then watching Avi's walkthrough, then watching it again and again and again....

I decided I would build an app that interacted with the user to show them latest World Records. So the first thing I did was to figure out how to get (scrape) the info I needed from the site - this was challenging since I had limited knowledge on the syntax for parsing HTML with Nokogiri. Well, I managed that and was pretty happy with myself.

The most difficult part for me was setting up the environment:
Frustration first came when *bundle install*  showed an error "*The validation error was '"FIXME" or "TODO" is not a description*" ....  WHAT?!?

After some googling that was fixed in the .gemspec - pretty simple actually, but frightening at first.
A few more errors that were fixed with the help of Stack overflow and still my list of records was NOT printing out as I expected - seems like scraping did not work!
Here Avi's video helped (I rewinded it a hundred times)  - I had forgotten that I not only have to 'require' Nokogiri in the environment, but also to add_dependency in the .gemspec  :-))))  and voilà - the list printed out.
I have no words to describe how good it feels to put the code to work!

From that point on I felt like the King of the World - I was in control and the app was behaving as wanted and expected.
I am sure I have to do some refactoring, but hey - better DONE than PERFECT, right!

