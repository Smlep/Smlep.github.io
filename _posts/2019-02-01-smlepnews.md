---
title: 'SmlepNews: A simple program to gather news from various apis'
layout: post
categories: jekyll update
---

Context
-------

During January, I had a lot of spare time compared to what I usually have: I
had just finished my fourth year intersnhip and was waiting to really resume
the lectures I had at school.

So I decided to work on another small project because I really enjoyed working
on my last open-source project during my spare time (you can take a look at
what I wrote on [SpacingChecker](/jekyll/update/2018/09/12/spacingchecker.html)
a few months ago).

Finding what to work on
-----------------------

The first main step of working on this project was to find what project it
should be. All I knew is that I wanted to work on something different from
[SpacingChecker](/jekyll/update/2018/09/12/spacingchecker.html), that meant
no complex regular expression checking in shell, and more precisely no shell at
all.

I didn't really have more constraints or things I did not want to do, so that
left me with plenty of choice about what to create, so I started to think about
what I thought I needed.

A few months before that, I started to be interested about startups and new
tech products, so I tried to made an habit of staying up-to-date with tech news
and innovations.

To do so, I spent a few minutes a day on
[Product Hunt](https://www.producthunt.com/) and
[GitHub](https://github.com/explore) and I found some really interesting
products and open-source softwares that I still use today (like
[f.lux](https://justgetflux.com/) for example). In the beggining, I really
enjoyed that, but after some time, some day it really started to feel like a
chore and it became hard to stay up-to-date.

So I decided to create a tool which would make this easier for me, and that's
how I started my own news agreggator.

Preparation steps
-----------------

From where should my news come from?
====================================

First, I did a small list of what I wanted to have in my aggregator first, and
what would be nice to have if I had enough time/motivation:

- [Product Hunt](https://www.producthunt.com/): A must have for me, a good
  place to find new softwares and websites.
- [GitHub](https://github.com/explore): The GitHub's explore section is really
  nice to stay updated with the last big open-source projects.
- A way to have global world news, not only tech because geek life can only
  get you so far :wink:.

What technologies should I use?
===============================

So, in the end, what I had to do was make calls to some apis, and maybe do some
scrapping, and then find a way to bring these information to me easily (command
line tool, website, or e-mails were the first way I thought about).

Python seemed like an obvious choice to me, since I knew well this language, it
was going to be easy to make calls to an api, to scrap websites, to send
e-mails or even to display the information I gathered on a website (I had a
good Django background).

Moreover, I enjoyed writing code in Python for some popular reasons such as the
ability to write code fast and easily, the light syntax and the huge amount of
already existing packages.

