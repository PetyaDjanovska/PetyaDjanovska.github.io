---
layout: post
title:      "Sinatra Project Mode"
date:       2018-06-25 14:33:14 +0000
permalink:  sinatra_project_mode
---


So Sinatra section made it clear how web apps actually work.
The project that I came up with was fairly simple as a idea - a Favorite Campsites app, where users can sign up, log in and keep a list of the places they visited or they would like to visit. Mainly there are two classes Campsites and Users that have many-to-many relationship. Campsite has a "created_by" attribute, so that it knows who created it. In this way I meet the requirement that only the creator should be able to update or delete the entry.
So far, so good - using ActiveRecord makes it even easier, so I did not have to worry about attribute accessors and stuff.
I gues the most exciting part was trying to architect the app, so that it is intuitive and well-structured. I must say I am not extremely satisfied, but for a first web app - I think it is OK :-)

The models:
In order to make sure that no invalid entries are made to the database, in my User class I used the following validations: username, presence: true and :username, uniqueness: true. Also in order to be able to implement sign up, log in and log out the User model "has_secure_password".
Also while testing I realized that the index of all campsites was not pretty if a user created a campsite without name, so I added ":name, presence: true" validation to the Campsite class. And of course it is not nice to fill up the database with the same campsites, so ":name, uniqueness: true" came right after.

The controllers:
There are three controllers - Application, Users and Campsites controllers. Users and Campsites inherit from Application. I did not forget to mount them in the config.ru, so there were no surprises there :-)
Create action were implemented in both Users and Campsites controllers, while update and delete only in the Campsites controller.

The views:
I wanted to use Rack::Flash to show some messages to the user depending on his requests and there was a bit of a cahllenge since I did not find a way to load the message first and then render the view I redirected to.

The challenges:
As I already mentioned the greatest challenge was the proper architecture of the app and I ended up adding a lot of functionalities after I tested the app and found out that I actually forgot sth. For example - the models have a many-to-many relationship, which means that a User can have many campsites, but I was so concentrated on implementing the create, update and delete functionalities that I complete had forgotten to give the User an option to add a place from a list of existing ones, WOW what a miss! Happily I noticed it before submitting and I added the function.

As a whole GREAT EXPERIENCE and many thanks to the technical coaches and lead and the fellow students who are always there to help!
