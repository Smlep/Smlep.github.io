---
title: 'Building a three-player chess website'
layout: post
categories: jekyll update
---

Context
-------

Around the end of 2019, as we were going through our few last months of
engineering school, we ended up having a quite consequent amount of free
time due to the highly irregular organisation of courses throughout the year.

Daniel, a friend of mine from school who has
been a huge fan of chess for a while now told us one night about how he read 
about this chess variant with three players and how he thought it would be
interesting to build a game engine for it.

Since I had time to ~~waste~~ spend building something ~~funny~~ meaningful,
I was interested in getting involved in this project to make it grow and be
something more than only a game engine (which I thought nobody would use
anyway, since playing chess through command line on a single computer does not
seem that appealing).

That's how, Daniel, Vincent (another friend from school with whom I had
worked on many side projects), and I decided that we were going to build a
website so that people could come and play chess with two of their
friends.

What is three-player chess?
---------------------------

Some might wonder what really is 3-player chess, do the rules change
when introducing a third player, and if they do, how?

Even though 3-player chess seems like a simple and precise concept, there are many variations
with light differences and not one set of rules for 3-player chess. These different
variations come in variants with different names (Trichess, Chess for three, Three-Player
Chess, Yalta chess...) but not every mention of one variant describes the same rules and
there is a huge lack of norm here.

The variation of chess played on [yalta-chess.com](https://yalta-chess.com) can be
considered as a unique variant, but mostly inspired by **Yalta Chess** (not much suspense
here) from which we tried to follow the rules as much as possible, but once again, the rules
differed depending on the articles.

On our website, you'll play on a 96-cell board (32 for each player, just like usual chess).

![Yalta board](/assets/yalta-animation4.gif)

The moves are the same as classic chess, but it can take some time to get used to the
moves around the center or the board when starting to play **Yalta Chess**. The only real difference
with 2-player chess is how winners and losers are handled.

The winner is the first player to checkmate another player, meaning that there are one
winner and two losers. This makes the game more interesting, rewarding aggressive strategies
since playing too defensive might end up in a loss where one of the other players checkmated
the third player.


Early development
-----------------

Our initial goal was pretty simple and seemed easy to accomplish, the
tasks which needed to be done could have been summed up as:

- Building a game engine, implementing every rule and move.
- Having a game page on which 3 players could play together with a decent user
experience.
- Having a basic matchmaking system, so that players could join games easily.

It looked easy and fast, the game engine was the main challenge since the special
shape of the board made the classic 2-player chess implementation unsuitable for
our needs and we needed to come up with a smart way to handle the board. Once the
game engine was out of the way, the only remaining thing would be to build a simple
website with basic functionalities.

Two of us already had some web development knowledge which we acquired through previous
side-projects, I would not say that we were **amazing** (or good) web developers,
but we were at least decent. Well, for the backend at least, our UI/UX level was (and
still is, but those who saw the website already know that) pretty bad.

Since we weren't looking for high performances in our game engine because a few
milliseconds were not going to impact the user experience, building the engine was
actually pretty fast. One of us focused on it, and after a few days we had a game engine
implementing the rules and about everything we needed except *promotions*, *castling*, and
*en passant* which came later.

Our implementation relied on the fact that instead of using one 8x8 board as in 2-player
chess, we considered the board as 3 distinct 4x8 sub-boards, each sub-board filled with a
different color on the example below: 
![Yalta debug mode](/assets/yalta-subboards.png)

The website, on the other hand, was way more complicated than we anticipated, handling
concurrent plays with real-time information transfer between the players (without
refreshing after each move) and implementing a decent user experience was much more
challenging than we expected.

Our first playable version looked like this:

![Yalta debug mode](/assets/yalta-debug.gif)

With the three boards representing the three sides of the board as explained above.

This first version allowed us to check that our engine worked as intended, but
required us to refresh a page to see the other players' moves and wasn't very user friendly.

That's when we really became aware that the website part of the project would require
an amount of work strongly higher than the game engine implementation.

A basic project
---------------

The more we implemented new features on our website, the more features we thought about
which seemed to be required to have a decent user experience on the website. Some of these features
were not necessary but seemed like good ideas/interesting to implement so we implemented some of them
and the others were listed and put aside for later.

After a few weeks, we had a decent result for the play part of the website; three players could
play on the same page, moving by selecting a piece and moving it to its location and seeing the actions'
results in real-time.

Our first *matchmaking* system was fairly basic, there was a list of created games, and any player
could join any game, if the user was the third player to join a game, it would start, and if there were
3 players already in the game, the user would be considered as a spectator. On top of that, any user
could create a new game.

At this time we had already spent way more time on this project than we thought we were going to,
even though we had only implemented the features we thought were necessary to have a good time
playing the game. The website's current state was enough to send the link to some friends and play
games with them if we wanted to, the global design of the website wasn't nice, but playing stayed pretty intuitive.

![Landing page](/assets/yalta-landing-1.png)

Not so basic anymore
--------------------

When we started this project, we did not define the real scope of users who would use it,
the more we worked on it and the more features we started implementing, the more we started to
want to make it public so that everyone could come and play.

As we started having less free time due to school projects and then the real jobs we got
after graduating, we spent way less time developing this project the following months but we kept working
on it and added a lot of new feature. Some of those being necessary for a public release,
some that we felt were a really nice addition for users and some which might just be
really useless (Hello, in-game chat). Among these extra-features are:

- A custom game system to play with friends with custom settings
- A public queue system to play with random unknown players
- A training mode to play against bots in different difficulties
- A profile system with ranks, elo, skins, themes, and statistics
- Game timers
- A board rotation system, to see the board as one of your opponents
- An in-game chat
- The possibility to show replays of games
- A documentation section to explain the website and the game rules
- A landing page to explain to new users what happens here
- A new implementation of the game engine with improved performances
and a graph system (replacing the 3x4x8 sub-boards implementation)

And of course, a landing page to welcome new players to our website.
The old matchmaking system based on a game list was removed, since the public
queue and private game system fully replaced the need for it.

![Ways to play](/assets/yalta-ways-to-play.png)

Costs and revenues
------------------

As we added new features and new services which started to increase potential costs, we had to
consider the *business* aspect of the website. We were not fully against trying to monetize it but
we did not want this to impact the user experience, driving potential users away because of
*aggressive advertising* or *pay-to-win* systems.

We considered **ads**, but generic ads (such as adsense) would require to have a huge 
amount of traffic to really generate money and they usually don't fit well into a website. We did
not want our website to get significantly less enjoyable for users just to win a few euros every month (or year).

<!--
Another thing we considered was to bring premium content to the website, allowing users to purchase
differents assets such as skin. The issue with this solution is that it is really hard to find good
content which will not impact the other users impact experience.
We did implement a skin system, so that players could update the apparences of their pieces, so that
we could set up a system where the users would be able to buy these apparences. But the impact on the
other players which were just trying to focus would be too high, who wants to start a game and be
matched again a player with flashy purple pieces?
There are options to prevent this scenario such as adding a button to hide every opponents skin, but
players won't buy skins if the other players can't see it.
-->


We considered some other solutions than ads but in the end, **we did not find an adequate business model**.
Not being able to generate revenue is not currently an issue, since the goal never was to quit our jobs and
start working on this project every day of the week. Nevertheless we did not anticipate when we started this
project (before we decided to add many unexpected features) that there were gonna be real costs to run
the website.

Indeed, the website now runs using many different services and tools which come with a cost, meaning
that we cannot sustain with this business model (which is not one, since we generate no revenue) if
our user count grows too much.

As long as our monthly costs stay under a few dozen of euros, it is
fine, I'd say that we are happy to pay for it if some people are happy to play on
[yalta-chess.com](https://www.yalta-chess.com/). But if this website became too popular, we would have
to scale up the different services we pay for (hosting, Redis, database...), resulting in hundreds of
euros bills.

Hence, if too many people end up enjoying our website, at some point we will have to **shut it
down** (or strongly restrict traffic) if we still cannot generate revenue.

This is really **unlikely** to happen since we don't plan on doing real advertising for this project,
and we are not so presumptuous as to think that this website is good enough to deserve this much 
success. But we still have to consider this scenario, and if it happens we will still try to consider
ways to generate revenue, we are not fully closed to ads, but we feel like right now nothing fits our
needs, maybe we'll set up a donation  system but those rarely work.

![Profile page](/assets/yalta-profile.png)

What's next
-----------

We probably spent too much time on this website, way too much, but most features were
implemented because we **enjoyed** it and not really because we felt like all of them were required.

We still have dozens of ideas about improvements that could be implemented for this project which
could make me work on this project for a few extra months or years.
But I thought it was time to wrap it up and prepare everything needed for a public release, putting
all remaining ideas into an issue list with implementation ideas if a **V2** came to be
implemented one day.

This will make this project feel like a *complete* product (even though I know it's not), allowing me
to move on to other side-projects.

<!--
Of course I know that releasing the website cannot mean that my work on it is over and that I can
fully stop working on it, because if it gets some success, I'll have to spend hours monitoring it
and fixing bugs, and even though we tried to build it to scale, it never is that easy.
-->

Come try the website at [yalta-chess.com](https://yalta-chess.com), if you don't find any players
in the public queue and you don't have any friends to play private games with, head to the
[training section](https://www.yalta-chess.com/private-queue?toggleTraining=yes)
(Create a custom game => Training) and try playing against our bots with various difficulties.

A special thanks to [Daniel](https://github.com/danielbaud) and 
[Vincent](https://github.com/Choqs) for working with me on some parts
of the project and for their continuous reviews of the website's progression.

If you want to get in touch about this project, feel free to contact me at smlep@yalta-chess.com.