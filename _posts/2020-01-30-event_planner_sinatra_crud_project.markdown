---
layout: post
title:      "Event Planner Sinatra CRUD project"
date:       2020-01-30 19:09:14 -0500
permalink:  event_planner_sinatra_crud_project
---


This project was so much fun to work on. I guess this whole curriculum about Sinatra was really fun. I was excited to finally be able to create a webapp.

So I decided to make an Event Page Website generator. Where a User can CRUD an event and add guests to the event. The guest then can visit the event page and RSVP to the event. The guest can also learn more about the event using the navigation links on top of the page.

Creating the project went pretty smooth till I got stuck on getting an association down between guests and events. I had written down some notes about the associations but for some reason I still couldn't see how to get it work.

```
User has many guests
User has many events

guest belongs to user
guest has many events

event has many guests
event belongs to user
```
I kept staring at this wall of text and kept asking how? I laugh now cause it was right there in my face. I asked an instructor to take a look at it and said you need to make a many-to-many relationship between guest and events. "guests has many events" and "events has many guests."

I felt so dumb at that moment. I don't know how I didn't see that. Anyways, it's always good to have a fresh pair of eyes.

So I created event_guests join table and at first I created it as a has_and_belongs_to_many, but learned that this method doesn't leave room for future growth. Which leads to my next problem.

So the whole point of this project was to let a guest visit your event page and RSVP to your event.

I couldn't figure it out. I've searched for like 2 days and couldn't find a solution. My instructor couldn't figure it out either.

With that said, I'm still happy with the way my project turned out. This is not the end of this project. I see myself using this project in the future. Wedding, perhaps? So, this is me, making myself accountable to get this feature implemented in the future. But, for now, I'm ready for RAILS!
