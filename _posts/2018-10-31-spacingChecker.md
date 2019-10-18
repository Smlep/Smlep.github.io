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
a **Merge Request** on our GitLab and I (or the other guy who is also in charge
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
tool to be able to fast check if someone made this kind of mistake.

First part: The few hours long project...
-----------------------------------------

At this point, I wanted to create in **a few hours** a light program to display
the spacing mistakes in a text, so I chose which technologies I would use
accordingly.

I could have gone for Python to have a program which would parse a file and try
to find how spaces were set around punctuation or maybe the same thing in C or
C++ which would be harder to create but would have way better performance. But
I didn't care about the performance, It didn't matter to me if checking a text
file would take 0.002 second or only 0.1 second so I did not go for C or C++.

When I started to think about it, the easiest way to detect these errors would
be to parse my file with **regular expressions** (which I'll call **regexs**),
so I decided to go for the simplest way I knew to match regular expressions in
file: [grep](https://www.gnu.org/software/grep/).

[grep](https://www.gnu.org/software/grep/) is a simple way to find lines
matching a pattern in files, what I had to do was to create **regexs** which
matched the spacing errors, feed them to `grep` with the files I wanted to
check, and that was it: a few hours work!

So I started to implement this simple shell program, I decided to first write
the rules for French, knowing that I would do the same for English after that.

To have a flexible program, I chose to store the languages configuration in
different files, which I called language files, I gave them the `.lg`
extension.

My program was then divided in two files: the language file for French
(`french.lg`) which looked like this back then:

`
 ,
 \.
[^ ]?
[^ ]!
[^ ];
[^ ]:
`

And the checker (`check.sh`) which consisted in a loop going through my
language files to then call `grep` on the target file with each **regex**
contained in the language file.

A few minutes and commits later I had the English language file ready, the
French language file had been improved so I had reached what I wanted to
have in the beginning: a simple program to detect some spacing errors in text
file in English or French.

My repository at this point can be found
[here](https://github.com/Smlep/SpacingChecker/tree/4cd6cc179914720c0059dd7588f742f56cd4bdce).

But, by the time I had reached this point, I already started to have many new
ideas for this program. Most of them were pretty simple or useless, but I
wanted to improve my [SpacingChecker](https://github.com/Smlep/SpacingChecker),
so I continued to work on this.

Second part: Making this program full
-------------------------------------

The first thing I wanted was to have options, so that this program could be
used in many situations, at this point I already had a simple `--help` option
but I decided to add a few more and to change how I implemented `--help`.

Help
====

Since I was beginning to have a big `README` file which described how my
program worked, I realized that the best solution for me would be to simply
display the content of my `README` when someone would trigger the `--help``
option. It seemed like a good solution back then, but now the `README` got
pretty huge, so I might need to rewrite a true help function in the future.

Silent
======

The silent option, triggered with `-s` or `--silent` would hide everything
which should be printed on the standard output, so that the only way to know if
the program found any errors would be to look at the exit code.

I implemented that the simplest way I knew how (there might be a better
solution) is by redirecting the standard output in `/dev/null`.

The resulting [code](https://github.com/Smlep/SpacingChecker/blob/master/check.sh#L135)
looks like this:
`
if [ $SILENT -ne 0 ]; then
  exec 1>/dev/null
fi
`

Languages
=========

At this point, I had changed the structure of the languages files, it was not
only a list of regex anymore, but there also was a **name** for each file and a
**short name**, so each `lg` file started like this:
```
# Name: French
# Short: fr
```

And if we wanted to check a file name `test.txt` in French, we could call
`
$ ./check.sh fr test.txt
`

This made the syntax lighter than when we had to give the language file path.

To display the list of the short names for the available languages, the
`-l`option was created.

`-l`, `--lg`` or  `--languages` display every available languages and their
short names:

```
$ ./check.sh -l

Short names for available languages:
fr: French
gb: English (GB)
de: German
it: Italian
us: English (US)
```

Once I had the language file structure figured out, I added more language files
(right now, there are `french`, `gb_english`, `german`, `italian` and
`us_english`), and kept improving the regular expressions for each languages.

So, I added support for ellipses (`...`), time (`hh:mm`) and decimal numbers
(is it `3.14` or `3,14` in this language?). This is why I had to split GB
English and US English.

Deploying my checker
--------------------

After adding a few options and three more languages my check was now way bigger
than what I expected to create in the beginning. My `check.sh` which contained
the shell script I used to perform the checking just went from 13 lines to more
than 150.

To feel like what I created would not be a 100% useless, I tried to make it
easy to use for anyone, because at this point, it might seem easy to use, but
it was annoying to install.

To run the checker, you had to clone the
[repository](https://github.com/Smlep/SpacingChecker) and then call the checker
from withing the repository. To make it easy to install I decided to add it to
a real package manager.

The only package manager I really used being
[Homebrew](https://brew.sh/), I wanted to do this one at least, and if it was
not too hard, then I would make it able to be installed with `apt-get` and
`Pacman`.

I won't explain all the different steps I went through to add SpacingChecker to
Homebrew, but it took me a way too high amount of time and of starting overs.
This was the first thing I tried to add to Homebrew (and probably the last one
:sweat_smile:) and it took me quite some time to make this work.

But in the end, I reached something and now it can be installed this way:

```
$ brew tap Smlep/SpacingChecker
$ brew install spacingChecker
```

Then, to use this from anywhere, juste call the `spaceCheck` command and
everything works.

```
$ spaceCheck us tests/theTortoiseAndTheHare.txt

Looking for a language file...
Searching files corresponding to us
Loading English (US)

Checking tests/theTortoiseAndTheHare.txt:

No error found in tests/theTortoiseAndTheHare.txt
```

Adding SpacingChecker to Homebrew really blow off my motivation, so I decided
not to add it to `apt-get` or `Pacman` for now, but I might do it in the
future.

Conclusion
----------

This is still a work in progress...
-----------------------------------





The source code for this project can be found
[here](https://github.com/Smlep/SpacingChecker), you can
leave a star if you find it useful :blush:.
