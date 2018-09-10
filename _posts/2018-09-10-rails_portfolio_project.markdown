---
layout: post
title:      "Rails Portfolio Project"
date:       2018-09-10 18:00:29 +0000
permalink:  rails_portfolio_project
---

RVroute is an MVC web app built using Rails 5.2.0. Basically this is a recreation of the same idea used in the Sinatra project.

**The models**
There are four models: User, Campsite, Favorite and Comment.
Favorites is a joint table, enabling a many-to-many relationship between User and Campsite, so users have many campsites *through* Favorites and campsites have many users *through* Favorites.
Comments belong to campsites and belong to users.
Attribute :name is validated for presence and uniqueness in the User and Campsite models. User has additional password_confirmation validation and uses has_secure_password.
In the Favorite model the need of a custom validation appeared, so there is a method #no_repeat_favorites to guard against duplicate favorite entries.

**The controllers**
All controllers inherit from the Application controller which implements logged_in? and current_user helper methods a callback *before_action* #require_login and #protect_from_forgery method.
*UsersController* which takes  care of the creation of new users utilizes two skip_before_actions: #require_login, only [:new, :create] and :verify_authenticity_token, only: [:create]. The second was added to fix an error "invalid authenticity token" error  when registering a new user.

*The SessionController* holds the logic for regular and Google login. The "omniauth-google-oauth2", "~> 0.2.1" was used here.

I've tried to keep the controllers thin :-)

**The class method**
In the Favorite model a class method #most_favorite was created and the controller has an action with the same name corresponding to a view presenting the one campsite that most users added to their favorites, this is basically how the *best_campsite* link works.

**The views**
Two layouts were used *Application* and *no_nav*. Partials utilized where appropriate. Form_for helpers to build the forms for user input data.

**The nested resources**
Comments were nested under the campsites route like so : */campsites/1/comments* which is linked to an index view showing all available comments on the given campsite. There is also the option to build a new *comment* from */campsites/1/comments/new* 

Hopefully this app will be developed into a more complete application with the ability to navigate the user to a selected campsite!


