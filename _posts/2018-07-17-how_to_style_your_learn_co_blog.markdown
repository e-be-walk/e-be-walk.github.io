---
layout: post
title:      "How to Style Your learn.co Blog"
date:       2018-07-18 02:20:05 +0000
permalink:  how_to_style_your_learn_co_blog
---


The general impression that I've gotten is that many students don't realize they can or know how to style their learn.co blog. If you're new to Flatiron, bootstrap, or using a github.io blog and hope to learn more about integrating changes within your blog let's take a look at how to make that happen.  

You may have noticed that your blog with Flatiron comes equipped with some stock images- one photo for your "about" page and a different one tops your blog index and each of your posts. Both images are filtered a clean, slate blue- your about page features an image of some strangers that appear to be intently working at something and the one within your blog index and postings is a angled view of a computer with some random code. It looks something like this:

![About Page of Flatiron blog](https://imgur.com/D6Kahra.jpg)

Maybe stylistically, these work for you but I find something a little off-putting about having some strangers on my about page and some random, blurry code I know nothing about topping my technical posts. That aside- it just plain doesn't match the wireframe I hope to implement in my portfolio. My hope is to continue to use my [learn.co](http://learn.co/blog) blog even after my experience with Flatiron so that I can continue to work on my technical writing and my articulation about code- both of which could use improvement. With my future portfolio and continued blogging in mind, I set about making some changes to my blog.  I found that [Flatiron's FAQ](http://help.learn.co/blogging/blog-settings/can-i-edit-the-css-of-my-blog) answered that change was indeed possible, but lacked an in-depth answer about how to actually make changes. 

Without reinventing the wheel and the entire bootstrap css you can implement some small changes that make a huge impact. Take a look at what my about page looks like now:

![My about page within my styled blog](https://imgur.com/tigDhpU.jpg)

Personal feelings about my choices aside, you have to admit- this is impactful change with some very easy fixes- namely fonts and images. So how do you go about doing the same to your blog? Once you've created a Flatiron Blog once your first post is made and published if you go to your github account, you'll notice there is a new repository: `:username.github.io` (substitute `:username` with whatever your github username actually is). Through github you can clone the repo and make some changes by clicking on the clone button of this repo in the top right, copying the link and running `git clone git@github.com:username/username.github.io.git`, from there `cd ./` into your repo and open it with `atom ./` 

You can easily change the heading images for your about page. Simply copy whatever image you wish to have from it's location in your file to the `img` folder within your `github.io` repo. Whatever title your image has must be the title used in the "header-img" at the top of your about.html page. Here's what it looks like in my editor- in this case, the image I am using is entitled "hero.jpg". You can apply the same fix by adding a `header-img` to the top of your referencing the image you want to use. If you want to change the picture from something other than your about your image, just repeat the steps copying the image file to your `img` folder and supplying the correct file name path within your `index.html`.

![about page image](https://imgur.com/1BjjZ8f.jpg)

One other quick fix I applied was to the fonts within the css. You can always go to [Google Fonts](https://fonts.google.com/) to pick your own font-families. I chose a fun decorative text for my headings and larger text complementing it with simpler, cleaner fonts for larger bodies of text. You'll want to `@import` your font files to your `/layouts/default.html` between script tags:
```
<!DOCTYPE html>
<html lang="en">

{% include head.html %}
<style>
@import url('https://fonts.googleapis.com/css?family=Abril+Fatface|Raleway|Trocchi');
</style>
<body>

... 

``` 

Then you'll open up your `css/clean-blog.css` and start substituting your own font-family for their values. The easiest way to do this is to press `cmd + f` to open the finder within your editor and type `font-family` in the search value. Then simply replace the font-family they list with the family you want.

![Changing fonts in css](https://imgur.com/uDtFokG.jpg)

So there you have it. It doesn't completely reinvent the functionality or layout of your blog but it makes a big difference in the overall appearance of your flatiron blog.  

*Note* Before you can see any of your changes live, you must commit and push your changes to git. In addition, it appears that when you make a new blog posting via the learn.co/blog dashboard, you will have to pull your new blog postings into your repository to see the styling changes applied by `cd ./`-ing into your repository, running `git pull` and `git push` in your console. 




