---
title: First post
author: Jubobs
---

# Code layout matters

Ah... code formatting! A contentious issue if there ever was one!
Most programmers likely do not give code layout much thought and are quite
content to adopt whatever style their IDE defaults to.
Some vigorously dismiss code layout as inconsequential
("Ultimately, the machine doesn't care!").

Many respected figures in the software community attach at least some importance to code layout.
Rob Pike and Brian Kernighan, in TODO, insists that a neat layout
contributes to the clarity and simplicity of the code:

> Code should be clear and simple—straightforward logic, natural expression,
> conventional language use, meaningful names, *neat formatting*, helpful
> comments—and it should avoid clever tricks and unusual constructions.

(my emphasis)
even though they concede that consistent use of a formatting style matters
more than the specifics of the style used.

Steve Freeman writes

> There's research suggesting that we all spend much more of our programming
> time navigating and reading code—finding where to make the change—than
> actually typing, so that's what we want to optimize for.

and describe how a layout can be _expressive_.

And Kevlin Henney certainly holds a strong opinion about (TODO) the importance
of code formatting: (TODO)

Although it is true that the machine doesn't care about how your code is laid out,
code layout does matter to human agents. Programming is an act of communication,
with current and future collaborators (including yourslef

# What about diffs?

# Inexpressive diff
``` diff
public final class ConferenceTalk {

    private final String title;
    private final String speakerName;
+   private final String description;
    private final LocalDateTime start;

-   public ConferenceTalk(String title, String speakerName, LocalDateTime start) {
+   public ConferenceTalk(String title, String speakerName, String description, LocalDateTime start) {
        this.title = title;
        this.speakerName = speakerName;
+       this.description = description;
        this.start = start;
}
```
