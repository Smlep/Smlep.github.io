---
title: 'SpacingChecker: New languages, multiple file checking and Homebrew installation'
layout: post
categories: jekyll update
---

I'm back a few weeks later with more updates on [SpacingChecker](https://github.com/Smlep/SpacingChecker). I've been working on it for a good month now and this project is coming to an end.

New features
------------
When I wrote my last post, [SpacingChecker](https://github.com/Smlep/SpacingChecker) was supporting French and English. 

Now, German and Italian are supported and English language was split between American English (Us) and British English (Gb) since there are a few small differences which are mostly about hours displaying.

More options have been added:
- ```-h```, ```--help``` display help
- ```-s```, ```--silent``` do not write anything to standard output
- ```-l```, ```--lg```, ```--languages``` display available languages and their shortnames

```
$ ./check.sh -l

Short names for available languages:
fr: French
gb: English (GB)
it: Italian
us: English (US)
```

Multiple file checking has also been added:
```
$ ./check.sh language file1 file2 *.txt
```

Installation
------------
Because cloning a git repository and using the program from the repository is pretty annoying , I've added an homebrew tap, so you can install it with homebrew and use [SpacingChecker](https://github.com/Smlep/SpacingChecker) as ```spaceCheck```:
```
$ brew tap smlep/spacingchecker
$ brew install spacingchecker
$ spaceCheck gb abritishfile
...
```

What's next
-----------
These last weeks have been dedicated to adding many small features to this program, even though the checker has looked finished from a while, I'll add a few more features and then I will be done with this if I don't find more interesting features to add. 

In the end, I'll write a post to explain why spend so much time on project with such a small utility (I could have had a checking has efficient with 3 times less work) and why this was not a waste of time.