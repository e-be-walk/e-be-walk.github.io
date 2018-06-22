---
layout: post
title:      "Off the rails"
date:       2018-06-22 02:46:09 +0000
permalink:  off_the_rails
---


My rails project took considerable gusto. Figuratively speaking, things have gone a little off the rails. Things have been crazy at work- I’ve either installed and de-installed 10 different galleries at work. Frozen pizza is consumed in my house no less than two times per week. And generally, the cleanliness of my house, deportment, and all things is on the decline. 

Despite the fact that I’m tired- and I mean, really tired- I’ve found myself moonlighting, working on my project well past my bedtime. Work provided me with the context, insight, and subject of my project- I essentially set up a database for users to enter specific information concerning sites that contain Tiffany Stained Glass Windows. This project enabled me to learn more about a feature upcoming exhibit and flex my considerable experience working with object databases as I do at work. Although I can recognize the flaws in my project, it is something I am truly excited for and which will be used- even if in redacted/altered form- by my museum. 

I always like to try to include some things I’ve learned along the way, so here goes. 

* In my Sinatra Project, I realized that sometimes restarting a project is better off. I followed my own advice this time around and though my project didn’t fundamentally change, it was totally worth it. During the building of my project, I dumped a TON of garbage data into it, testing for functionality. I later decided to delete these files and went a little too far. I tried to revert to a previous commit and failed. Restarting my project allowed me to fix some things, work through things line-by-line, and just know my project so much better. It’s not ideal, but it was good practice anyway.

* Don’t be afraid to reach out for help. I can’t tell you how much having my little slack community helped to support me through this. Fellow classmates helped me when I was stuck, commiserated with me when I was tired, and pumped up the support as I meandered through this. These folks give me something to aspire to. 

* Bugs can be a lot harder to catch in rails- pay attention to the routes and urls that your program is following. With my nested routes sometimes things appeared to be working and when I looked closely things weren’t quite following- edits weren’t committing, links were mis-routed, and nested resources weren’t always going to the right place. Just because a view loads and doesn’t through errors doesn’t mean it’s ‘working’. 

* Try to keep in mind and research features you want your app to have ahead of implementing them. I knew I wanted to be able to upload images and implemented it immediately using the [paperclip](https://github.com/thoughtbot/paperclip) gem. I should have done the same thing for search functionality- many search gems like [pg_search](https://github.com/Casecommons/pg_search) rely on using Postgres instead of SQLite 3 and though migration is possible, I didn’t want to test that out in the last days of working on my project- it seemed like I would be tempting fate. 

* Work on something that interests you, relates to your life, or is something you enjoy. To be completely honest, I have zero interest in Tiffany Windows, but I do have an interest in neat old buildings, history, biblical depictions in art, contextual history and helping my museum. I may not be particularly interested in Tiffany Windows, but this project helped to solidify ways I can implement my code and I enjoyed learning about the area via the sites I was learning about along the way.

And without further ado, my Tiffany in Connecticut Stained Glass Repository can be found here: [GitHub - e-be-walk/tiffany-in-ct-v2.0: A reboot of my rails app.](https://github.com/e-be-walk/tiffany-in-ct-v2.0) 
