---
layout: post
title: Figuring out the Label and Caption in LaTeX
---

Sometimes, when you place the label and caption inside the figure out of order, you get 
weird numbering in your document when you go to reference that figure. What many people don't realize
is that there is a reason for this madness and it is much easier to understand why this happens, then
to try and remmember the order in which these things should go.

Why this happens
================

Perhaps if people know why this happens, it will be much easier to remember what goes where.

Short version
-------------

Caption command within a figure or table acts much like a sectioning command within the document. So if you don't put a caption, the label has nothing to "label", and the closest thing it can find is a section in which you are in.

Longer version
--------------

To understand what is going on we must establish a few things. First, a label command when placed anywhere in the document will label the section of the document in which it is places. So something like this:

    Section \ref{sec-one} is great!  

    \subsection{First section}
    \label{sec-one} 

    This is the first section

Will produce:

    Section 2.11 is great!

    2.11 First section
    This is the first section


Second, label command appearing in a *numbered* environment acts
differently. Numbered environments are things like equation, eqnarray,
enumerate, figure, table... In each of these environments the
label command acts differently. For example, in eqnarray
environment the label can go anywhere before the \\\\ that ends the
current equation - effectively giving each equation it's own label!

The figure environment has different rules. In particular, the thing
that creates numbering inside the figure environment is the caption
command. A figure may have multiple captions, creating multiple
"sections" within the figure. On other hand, if the caption command is
never used, the label still uses the text numbering (which is the
number of the section of the document it is in).

> **Remember**: A figure may have multiple captions

So, if we have something like:

    \begin{figure}
      BLAH
      \label{sec:one}
      \caption{Blah figure!}
      \label{fig:blah}
    \end{figure}

we now know that `Section \ref{sec:one}` will refer to the section of the document in the text and will produce something like `Section 2.11`.

While `Figure \ref{fig:blah}` will actually refer to the thing we want and will produce something like `Figure 1`.

Conclusion
==========

Since it is difficult to remember which goes first, caption or label,
inside your figure, understanding why the order matters completely
removes the need for memorization. Since the caption command is
responsible for sectioning the figure environment, we know that we must
call it at least once before using the label command.  By knowing the
why we can immediately deduce the how - and that makes all the
difference!

Reference
=========

I would be lying if I said I figured this *(no pun intended)* out on my own. The book "LaTeX: A Document Preparation System (2nd Edition)" by Leslie Lamport, as old as it is, was the primary source for my understanding of this topic.