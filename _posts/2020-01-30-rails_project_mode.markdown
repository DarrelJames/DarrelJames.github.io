---
layout: post
title:      "RAILS Project Mode!"
date:       2020-01-31 00:09:45 +0000
permalink:  rails_project_mode
---


For my rails project, I decided to use the same model I used in my Sinatra Project. I saw that the rails project requirements was literally everything I did in my Sinatra project. I didn't get to completely implement all the features I wanted in Sinatra, but I got it done in rails!

To Recap.

I created an Event Planner app where a User can sign up/log in. The user then can create Events. User can add Guests to their guestlist per event.

Guests can RSVP by going to the event's website and click on the RSVP link. This page will ask the guest to type in their first and last name. If the guest is invited to that event, guest will be able to respond via the form presented.

Creating this project on rails was so much easier and faster. Also, having worked with this Domain Model before helped a lot as I didn't have to think much about how to create the relationships.

 I utilize a few gems like Devise that handled the Authentication and CanCanCan that handled the authorization. These gems are amazing and very simple to install and get started with them.

  Rails is so much fun. I loved how fast and easy it was to make the forms. Also, the generators!

  `rails g resources`

With this one command you get the MVC architecture generated for you.

With over 150 thousand lines of code in rails. There is still so much to learn.

Check out my project here
https://github.com/DarrelJames/rails_event_planner
