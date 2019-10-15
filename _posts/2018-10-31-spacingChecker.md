---
title: 'SpacingChecker: A huge tool to do one simple thing'
layout: post
categories: jekyll update
---

Context
-------

I have written some posts about
[SpacingChecker](https://github.com/Smlep/SpacingChecker) in the past to talk
about how the project was changing and what I was adding, but now that I think
I am done with it, it's time for a conclusion post to talk about what really
was that project and why it existed.

A few months ago, I started to have to this work in parallel with my studies
where, among other things, we write tutorials for students to help them learn
how to code. We are a small team working on it, and one thing I have to do that
others don't is reviewing what the people I work with write.

So, when someone wants to add a new paragraph in a tutorial, then he has to do
a **Merge Request** on our gitlab and I (or the other guy who is also in charge
of reviewing) have to review and merge if everything is fine.

Of course, everyone did spelling mistakes since we were all only getting
started with this job, but there was a kind of mistake that most people did
really often: adding, or not, spaces around punctuation. Should we put a space
before `:`? Is there a space after a `;`? And what about `!` and `?`, is this
the same rule?

In the end, the answer to this question were pretty simple, but the issue is
that it is language-dependent, most precisely, these rules were really
different between English and French.

But we were French students, writing English tutorials, so there was a great
deal of confusion about what rule to use, and that meant many mistakes.

I knew that eventually, these rules would stick and that nobody would make
these mistakes anymore, but it was going to take some time and I was getting
tired of leaving 20 comments on each **Merge Request** so I decided to create a
tool to be able to fastly check if someone made this kind of mistake.

First part: The few hours long project...
-----------------------------------------










The source code for this project can be found
[here](https://github.com/Smlep/SpacingChecker), you can
leave a star if you find it useful :blush:.
