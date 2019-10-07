---
title: 'SmlepNews: A simple program to gather news from various APIs'
layout: post
categories: jekyll update
---

Context
-------

During January, I had a lot of spare time compared to what I usually have: I
had just finished my fourth year internship and was waiting to really resume
the lectures I had at school.

So I decided to work on another small project because I really enjoyed working
on my last open-source project (you can take a look at what I wrote on
[SpacingChecker](/jekyll/update/2018/09/12/spacingchecker.html) a few months
ago).

Finding what to work on
-----------------------

The first main step of working on this project was to find what kind of project
I wanted it to be. All I knew is that I wanted to work on something different
from [SpacingChecker](/jekyll/update/2018/09/12/spacingchecker.html), that meant
no complex regular expression checking in shell, and more precisely no shell at
all.

I didn't really have more constraints or things I did not want to do, that
left me with plenty of choice about what to create, so I started to think about
what I thought I needed.

A few months before that, I started to get interested about startups and new
tech products, so I tried to make a habit of staying up-to-date with tech news
and innovations.

To do so, I spent a few minutes a day on
[Product Hunt](https://www.producthunt.com/) and
[GitHub](https://github.com/explore) and I found some really interesting
products and open-source softwares, some that I still use today (like
[f.lux](https://justgetflux.com/) for example). In the beginning, I really
enjoyed that, but after some time, some day it really started to feel like a
chore and it became harder to stay up-to-date.

So I decided to create a tool which would make this easier for me, and that's
how I started my own news aggregator.

Preparation steps
-----------------

Where should my news come from?
===============================

First, I did a small list of what I wanted to have in my aggregator, and
I knew I would add more features later if I had enough time/motivation:

- [Product Hunt](https://www.producthunt.com/): A must have for me, a good
  place to find new softwares and websites.
- [GitHub](https://github.com/explore): The GitHub's explore section is really
  nice to stay updated with the last popular open-source projects.
- A way to have global world news, not only tech news because geek life can
  only get you so far :wink:.

What technologies should I use?
===============================

So, in the end, what I had to do was make calls to some APIs, maybe do some
scraping, and then find a way to bring this information to me simply (command
line tool, website, or e-mails were the first solutions I thought about).

**Python** seemed like an obvious choice to me, since I knew well this language, it
was going to be easy to make calls to an API, to scrap websites, to send
e-mails or even to display the information I gathered on a website (I had a
good Django background).

Moreover, I enjoyed writing code in **Python** for some popular reasons such as the
ability to write code fast, the light syntax and the huge amount of
already existing packages.

Starting to gather
------------------

Once (almost) everything was decided, I was able to start gathering data.

Product Hunt
============

[Product Hunt](https://www.producthunt.com/) was the first website where I
tried to gather data, my goal was to get the links and information for the most
popular products each day so that I could easily see if I found any of them
interesting, and if I did, access to more details by following the link to the
owner's website.

Product Hunt gives the users access to an
[API](https://API.producthunt.com/v1/docs) which can be used to make
simple read-only requests as long as you have an access\_token. This token can
be obtained by creating an account and going to the [API
dashboard](https://API.producthunt.com/v2/oauth/applications).

Then, anyone can access the top posts of each day to gather the **names**,
the **taglines**, the number of **votes** and the product's **urls**.

GitHub
======

The second website where I liked to find news was
[GitHub](https://github.com/), I really like open-source and learning new
technologies, so I felt like going through the most popular repositories daily
would be a good way to stay up-to-date.

GitHub also provides an [API](https://developer.github.com/v3/) which does not
require authentication to execute read-only requests with a limit of 60
requests per hour. Of course, by being authenticated, you can execute more
complex requests and with more requests per hour, but for what I had to do,
there was no need to be authenticated.

What I did was requesting the most popular repositories from the last 24 hours
and extract basic information about them: the **names**, the **descriptions**,
the **authors** and the number of **stars**.

Global News: The Guardian and Le Figaro
=======================================

For the news, I first started to use
[The Guardian](https://www.theguardian.com/), since it has a nice
**API** which can be used by getting an API key by registering
[there](https://open-platform.theguardian.com/). The API is easy to use and has
all the information I needed on the articles.

But the thing with news is that it can only be truly relevant if it's localized,
and since I live in France, I needed to get news from a local newspaper.

So I chose to get news from [Le Figaro](http://www.lefigaro.fr/), which is
a French daily morning newspaper. Sadly, [Le Figaro](http://www.lefigaro.fr/)
does not provide any **API**, but it has its own *rss feed*
[here](http://www.lefigaro.fr/rss/figaro_actualites.xml), and parsing *rss
feed* is really easy with **Python** using
[feedparser](https://pythonhosted.org/feedparser/).

Weather
=======

While I was implementing the **API** gatherers, I had another idea for
improvement. One thing I do every day is checking the weather in the morning,
so I chose to add a weather gatherer.

The weather website I decided to use was the popular
[OpenWeatherMap](https://openweathermap.org/) which is well-known for providing
an easy-to-use and free weather API for over 200 000 cities.

This allowed me to get the weather for the next 24 hours with a 3-hour interval
which was accurate enough for me.

Displaying the data
-------------------

Once I had gathered everything I wanted, I had to decide how the results would
be brought to me and when.

The when was an easy question, indeed, I designed most of the **API** calls to
get information for today, so I decided that I wanted to get the results daily.

But how was a trickier question...

Command Line Tool
=================

The easiest thing I could do was to simply do command line calls to my
**Python** program and display the formatted output on my computer's shell
every time I wanted to have this information.

This is pretty easy, I simply had to write a few functions to format the data I
gathered from the different **API**s and have an entry **Python** file, which
once executed would make all the calls, format the output and display them to me.

With a few tricks, I could have made this as a simple shell command I could
call from anywhere (like `showNews`).

The issue with this solution would be that I would have had to open my laptop
and start the program each time, this is something I do pretty often, but the
goal was to get the news every morning easily, and opening my laptop is not the
first thing I do every morning.

Website
=======

The second solution I explored was to display the gathered data in a website,
so that I could read the news every morning on my phone, laptop or pretty
much anything with internet.

Deploying small websites is something I have done a lot, so I already had the
technologies figured out, [Django](https://www.djangoproject.com/) in the
back-end, classic **HTML** and **CSS** in front-end with
[Boostrap](https://getbootstrap.com/) to have something fast and not too ugly.

To deploy my website online, I would use [Heroku](https://www.heroku.com) which
I really enjoyed since it allows me to deploy free websites and I find the git
deployment really easy and smooth.

There were two issues (that I found) with the website solution.

First, it was a lot more work than what I was going for in the beginning,
because creating and deploying a simple website is still a consequent amount
of work if I want to do it well.

The second issue is that this program's goal was to be as light and small as
possible but turning this repository into a Django website was going to make it
way heavier than I wanted. Of course, I could keep this repository to only
perform the API calls, and design the Django website in another repository, but
another goal I had was to have everything in the same repository, so that was
not going to work.

Emails
======

The solution I chose to use was emails. This was pretty easy, I wrote a few
functions which formatted the gathered data to be easy to read in an email,
then I created a gmail account for this purpose, and using
[smtplib](https://docs.python.org/3/library/smtplib.html) I was able to
send an email to a target I chose.

But what I wanted to do wasn't to open my laptop every morning, run a
**Python** program and then go to my email reader to read the email I just
sent myself, this would just be a waste of time and would be like the *command
line interface* solution but more complicated.

What I needed was for these emails to be sent programmatically every morning,
no matter if I had access to my laptop at that time.

Another thing I wanted was to be able to send the email to multiple
targets, and to be able to update the target list *easily* without having to
alter my code.

So, I took a free [AWS](https://aws.amazon.com) **EC2** which I could easily
access through *ssh*. There, I cloned my repository, added my credentials and
added a local [PostgreSQL](https://www.postgresql.org/) database on which I
stored all the target emails.

So, every time I'd call `sender.py`, the calls to the **API**s would be made, the
results formatted and then an email would be sent to each target on the target
list.

And last, to be sure my server would trigger the **Python** package every
morning, I added a [cron job](https://en.wikipedia.org/wiki/Cron) for each
morning at 8 a.m., here's the content of my crontab (opened with `crontab -e`):

```
0 8 * * * ~/cron/news.sh 2>~/log/error.log
```

`news.sh` is a simple bash program used to call my `sender.py` file, I used
it to make some tests and I'm pretty sure it isn't required anymore, so I might
refactor this in the future.

Languages
=========

To speak briefly about the languages, since I was getting French articles from
[Le Figaro](http://www.lefigaro.fr/), I was not able anymore to do a full
English software. So I decided to have two versions of the sent emails: English
and French, the English one using [The Guardian](https://www.theguardian.com/)
and the French one using [Le Figaro](http://www.lefigaro.fr/).

Right now, the emails I send myself are in French, but the way I designed this,
it could be swapped by changing two characters in the code. In the future, I
might add the desired language in the database next to the target emails to
make this more flexible.

Results
-------

Now, each morning I get an email looking like this:
![French example
email](/assets/smlepnews_french.png)

And this is how the English version would look:
![Example email](/assets/smlepnews_english.png)

The email design is pretty poor in my opinion, but it brings me the information
I need each morning so I don't think I will try to spend hours to try to have
pretty emails since the email part is not the main purpose of this project.

To conclude, I really enjoyed working on this project and writing this post,
so I will try to find another small project of this kind to work on soon and I
might be back with another post of this kind.

Thanks for reading this!

The source code for this project can be found
[here](https://github.com/Smlep/smlepNews), you can leave a star if you find it
useful :blush:.
