---
layout: post
title: "Spooky Python"
date: 2017-10-31 19:44:09 -05:00
tag: python
---

# Spooky Python
## What is the craziest python feature you can think of?

At a Halloween party with my coworkers, the discussion turned to spooky python "features". I don't know if quirks in a language qualify as spooky but it is fun to think about the sometimes unexpected behaviors that you may run into from time to time. With that, some of my favorites are below.

### Fun with Unpacking
During PyCon 2015, David Beazley gave a talk on [concurrency](https://youtu.be/MCs5OvhV9S4). In the middle of the talk, DaBeaz wrote this:

```python
can_recv, can_send, [] = select(recv_wait, send_wait, [])
```

Of course, unpacking an iterable is a common task in python

```python
>>> a, b, c = 1, 2, 3
```

This makes sense and does what you would expect, setting a, b, and c to 1, 2, and 3, respectively. However, that's not what happened during the talk.

```python
>>> a, b, [] = 1, 2, []
```

This looks like an empty list is being assigned to an empty list. Obviously, that should not be possible. Something else must be happening.

```python
>>> a, b, [c, d] = 1, 2, [3, 4]
```

The third element is a list being further unpacked into two variables. From there, it's not a huge leap to see that the empty list is actually unpacking into another list that just happens to be empty.

### Boolean sums?
One of the craziest things I've run into is being able to add booleans.

```python
>>> True + True
2
```

What!? Why!? How!?

As far as I can tell, this is a holdover from a time before booleans were an official type in python. As recently as python 2.3, the types True and False did not exist.

```python
>>> True = 1 == 1
```

If you've ever seen code like this, that's what it is for. In more recent versions of python, the above code returns True. In earlier versions, True would be equal to 1. Therefore, allowing **True** to evaluate to 1 makes sense.
