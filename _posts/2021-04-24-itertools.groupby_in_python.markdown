---
layout: post
title: "Using itertools.groupby in Python"
date: 2021-04-24 16:53:17 +0200
categories: python
---
I came across an interesting problem on hackerrank.com: 

>how many characters have to be removed from a string like 'AABBBAABABABAABBB' to get a sequence like 'ABABABABAB'?

This problem can serve as a nice demonstration of `itertools.groupby` from python build-in's.
A one-line solution to the presented problem looks looks like this:
```
count = sum([max(0, len(list(g))-1) for k, g in itertools.groupby(list(s))])
```