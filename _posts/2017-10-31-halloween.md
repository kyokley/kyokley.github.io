---
layout: post
title: "Spooky Python"
date: 2017-10-31 19:44:09 -05:00
tag: python
excerpt: "Spooky Python: Unexpected Python Features"
---

# Spooky Python: Unexpected Python Features
## What is the craziest python feature you can think of?

At a Halloween party with my coworkers, the discussion turned to spooky python "features". I don't know if quirks in a language qualify as spooky but it is fun to think about the sometimes unexpected behaviors that you may run into from time to time. With that, some of my favorites are below.

### Fun with Unpacking
During PyCon 2015, David Beazley gave a talk on [concurrency](https://youtu.be/MCs5OvhV9S4). In the middle of the talk, DaBeaz wrote this:

```python
{% highlight python %}
can_recv, can_send, [] = select(recv_wait, send_wait, [])
{% endhighlight %}
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

### Boolean Sums?
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

If you've ever seen code like this, that's what it is for. In more recent versions of python, the above code returns True. In earlier versions, True would be equal to 1. Therefore, allowing **True** to evaluate to 1 makes sense from a historical standpoint.

### Non-existent Slices
I'm sure everyone has accidentally tried retrieving a non-existent index from a list before.
```python
>>> foo = []
>>> foo[0]
Traceback (most recent call last):
  File "<input>", line 1, in <module>
      foo[0]
IndexError: list index out of range
```
Not surprisingly, python raises an IndexError because we have attempted to step off the end of the list.

Slices offer a convenient way of accessing a portion of a list.
```python
>>> foo = [1,2,3,4,5]
>>> foo[2:4]
[3, 4]
```
Above, I'm returning the items of the list between 2 and 4. This is pretty basic stuff. But, have you ever tried slicing with indices outside the bounds of a list? It's not something I had ever thought to try until one of my coworkers mentioned it.

```python
>>> foo = []
>>> foo[1:10]
[]
```
Interesting, huh? The [python documentation](https://docs.python.org/2.7/tutorial/introduction.html) mentions this behavior explicitly.
```
...out of range slice indexes are handled gracefully when used for slicing
```
In other words, out of bounds indices are replaced by the min/max indices of the list.

### Small Integers in Memory
```python
>>> a = 1
>>> b = 1
>>> a is b
True
>>> a = 10
>>> b = 10
>>> a is b
True
>>> a = 100
>>> b = 100
>>> a is b
True
>>> a = 1000
>>> b = 1000
>>> a is b
False
```
That last result is a little odd. Turns out, python allocates memory for small integers immediately when the interpreter starts up. Larger numbers are allocated as necessary. I first learned about this behavior from reading [Kate Murphy's blog.](https://kate.io/blog/2017/08/22/weird-python-integers/) She goes into far more detail about this behavior. It's definitely an interesting read and you should check it out.

### Conclusions
There are a lot of language quirks out there. I hope you've enjoyed seeing some of my favorites. If you're interested in trying any of these out, I've tried them all in python 2.7 except for "Fun with Unpacking" which was pulled from Dave Beazley's PyCon talk in which he was using python 3.
