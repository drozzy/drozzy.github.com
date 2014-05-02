---
layout: post
title: Independence within the System
tags: [systems]
---

# The Problem

Consider a system shown on the diagram below:
![Connected](/images/independence/connected.png)

The question we want to ask is *what type of behaviour my the elements in B display so that subsystems A and C will be independent of each other*?

In other words, how much the subsystem B behave for the diagram to look like this:

![Disconnected](/images/independence/disconnected.png)

# Independence

Before we give an answer to the question above, let us first make exact what is meant by *independence*. Consider two arbitrary parts *x* and *y* of some larger system. Suppose we observe how *x* and *y* behave over time and notice that if we start *x* at some value *x=1* and *y* at some value *y=1*, then *x* will be *x=2* at the next time step. However, if we start the whole thing again at *x=1* by change the *y=3*, then *x* will be *x=77* at the next time step. From this we can concluse that the value of *x*, for this particular case, and in this time step *depends* on the value of *y*. We say that *x* is *dependent* on *y* from the given start states for a single time step.

Often, it will be noticed that *x* will depend on *y* for all time steps and for all starting states. In which case we say that *x* is *dependent* on *y*.

# Answer

# Conclusion


References
==========

1. W. Ross Ashby, Introduction to Cybernetics, 1956.
2. W. Ross Ashby, Design for a Brain, 1960.




