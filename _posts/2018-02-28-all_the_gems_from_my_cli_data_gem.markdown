---
layout: post
title:      "All the gems from my CLI Data Gem"
date:       2018-03-01 01:45:50 +0000
permalink:  all_the_gems_from_my_cli_data_gem
---


I was really excited to be working on this project. Working with the material and video tutorial, I felt like I was totally confident I could take this on and do a decent job. Although I am happy to say that I am writing this blog in preparing to submit this lesson, I have to admit that there was a strange, sort of shaky point or two in there. 

I watched the walkthrough video within the CLI lesson- which was amazingly useful and definitely a reference I used throughout the course of my project. I took a look at one of the resources that was pulled up in the demo- a video from  [railscast](http://railscasts.com/episodes/135-making-a-gem). I looked at a few fellow students’ blog postings about their CLI projects and found a great how-to [bundler](http://bundler.io/v1.12/guides/creating_gem.html”) doc. I listened to a [ruby rogues podcast](http://devchat.tv/ruby-rogues/291-rr-building-ruby-gems-with-brandon-hilkert”) all about gems. I felt like I had a good grasp on the prior lessons on scraping. I had an idea and I made copious notes. I attended a study group specifically for CLI data project prep. For all intents and purposes, I was pumped and felt prepared to take this on.

It seems like I had properly prepared for this. I looked at resources. The lessons incrementally prepared me for this. I knew what I was going to do and the information I wanted my gem to provide. And then I basically started screwing things up.

I should preface this in saying that I’m a part time student, a full-time employee, a part time employee, a dog mom, a tutor, and a reasonably driven human being. I do a lot, I work too much, and I’m no saint— I get tired. After working a ten hour day, eight weeks without a day off, and twenty-eight straight days of coding, I began my project. I was so excited to start on it that morning, it was difficult to force myself to go to work. When I got home, I fed the dogs, fed the boyfriend, and managed a quick change into my lazy pants and popped open my laptop. And then I did the unthinkable.

I sat quietly, in the only spare hour and a half I had and I dutifully laid out the file structure of my gem. Thus far everything was working and looked good. I managed to get a heck of a lot done in only that hour and a half… And I did it all without starting a GitHub repository. 

¯\_(ツ)_/¯

Somehow, I managed to nest all my files within the cli data gem learn ide repository. Silly as it was, it was a confidence-stifling, fairly large set-back given my available free time. It wasn’t my only set back, but rather than writing a novel-like play-by-play of all my minor failings and premature, mini panics I think it’s more productive to tell you what I wish I knew. 

Think about what you hope to do- more specifically, look at the websites you hope to scrape and try to inspect the elements you’re trying to scrape. Not all websites are created equally- and some of html elements and structures are downright confusing. 

I know it isn’t advised to use ask a question in this lesson. Because of time scarcity and limited one-on-one scheduling, I waited and spent A LOT of time trying make a feature work that would require a system call. I did not know that even if I could get it to work it would likely not work consistently from user to user based on system permissions.

Don’t feel like you have to know everything before you start. I spent a lot of time preparing and it was time well spent but I frequently went back, reviewed, and had to look up stuff throughout the process of building my gem. You’re not ever going to know everything in dev- I’ll have to get used to it- as long as you can look things up, you’ll be alright.

Look at the lessons following the CLI lab assignment. The learn curriculum page will pop up a red banner yelling at you for it and it’s likely the page will ask you if you’re sure you want to proceed menacingly, but the lessons after the CLI Project lab with additional walkthroughs, anti patterns, and student refactoring were ENORMOUSLY helpful once I overcame my fear of working ahead against the browser’s wishes. Because I reviewed those lessons after I had my gem mostly built and functional, I became really concerned my gem wasn’t going to be good enough- and I mean, it’s not great, but it works. I knew it wasn’t going to be a project where I was really “breaking the mold” and doing something crazy innovative. Had I tuned into those lessons prior to starting my gem, it’s likely I would have done more than a few things differently and maybe it could’ve been a cooler, more useful little gem. 

Without further ado, I introduce to you my CLI Data gem: [tech_news](https://github.com/e-be-walk/tech_news). It retrieves the three most recent headlines from Wired, TechCrunch, and the tech section of NYTimes and  then provides some additional details at the user’s request. I built it with the intent of learning more about tech because my background is anything but tech oriented. Upon building it, I find it unlikely that I will ever use it given that all of this information pops up on my magical, smart phone. Of course, this is pre-review so it’s likely some changes will be made but any suggestions in the meantime are welcomed.
