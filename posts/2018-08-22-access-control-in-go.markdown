---
title: >-
    Access control in Go: a primer for Java developers
author: Julien Cretel
published: 2018-08-22T21:30:00Z
---

Go supports multiple programming paradigms, including object orientation.
However, if you're coming to Go from Java, you may be slightly... ehm...
_disoriented_.
One striking absence is that of any access modifiers.
You may be wondering:

> Where are my `public`, `protected`, and `private` keywords?
> What mechanisms for access control does Go provide?

Fret not!
Access control in Go is simpler than in Java.
No access modifiers needed!

# Why Go needs, not four, but only two access levels

You're most likely familiar with the four access levels that Java provides.
I've listed them below, from the most to the least restrictive,
along with a concise description of their semantics:

* **private**: only accessible from the same class
* **package-private**: only accessible from the same package
* **protected**: only accessible from the same package and (direct or
  indirect) subclasses
* **public**: accessible from anywhere

(Note: The term "package-private" is nowhere to be found in the [Java language
specification][java-spec] but was popularised by Joshua Bloch in his book,
[_Effective Java_][effective-java].)

We've lined them up; now let's knock two of them down!

## Package as the unit of encapsulation

Go allows you to define concrete types—which in Java, would be _classes_—but

> [...] the unit of encapsulation is the package, not the type as in many
> other languages.

(source: [The Go Programming Language, Donovan & Kernighan][gopl], section 6.6)

For instance,

> The fields of a struct type are visible to all code within the same package.

(ibid)

Therefore, Go has no need for a distinction between _private_ and
_package-private_.
And then there were three:

* ~~**private**: only accessible from the same class~~
* **package-private**: only accessible from the same package
* **protected**: only accessible from the same package and (direct or
  indirect) subclasses
* **public**: accessible from anywhere

## No inheritance

Most notably, Go provides no mechanism for inheritance.
Therefore, Go has no need for a distinction between _package-private_ and
_protected_.
And then there were two:

* ~~**private**: only accessible from the same class~~
* **package-private**: only accessible from the same package
* ~~**protected**: only accessible from the same package and (direct or
  indirect) subclasses~~
* **public**: accessible from anywhere

# Access control in Go

We're left with two access levels, which is all Go needs:
public and package-private.
Go's terminology is different from Java's, though:
an identifier is said to be either _exported_ (public) or _non-exported_
(package-private).
You will likely also come across the term "unexported", which is an informal
synonym of _non-exported_, but
[I recommend using the more formal term][unexported-twitter].

For controlling access to identifiers, [the Go designers opted for naming
convention rather than verbosity][exported-identifiers]:

> An identifier is exported if both:
>
> 1. **the first character of the identifier's name is a Unicode uppercase
>    letter** (Unicode class "Lu"); and
> 2. the identifier is declared in the package block or it is a field name or
>    method name.
>
> All other identifiers are not exported.

(my emphasis)

To fix ideas, here is an example involving two package-level variables:

``` go
package foo

var (
    Bar = "Bar"
    baz = "baz"
)
```

Package `foo` exports `Bar`, because the first letter is uppercase.
However, `foo` does _not_ export `baz`, because the first letter is _not_
uppercase.

# Conclusion

[Go was designed to be easy to read][pike-talk], and the design decisions
around access control certainly contribute to Go's readability:
not only is the code unencumbered by pesky access modifiers, but the case of
an identifier's first letter is enough to know whether the identifier is
exported.

This is just one reason why you may find that reading Go takes less of a toll
on your brain than reading Java does.
But that's just my opinion. What do _you_ think?

[effective-java]: https://www.pearson.com/us/higher-education/program/Bloch-Effective-Java-3rd-Edition/PGM1763855.html
[exported-identifiers]: https://golang.org/ref/spec#Exported_identifiers
[gopl]: https://www.gopl.io/
[java-spec]: https://docs.oracle.com/javase/specs/jls/se10/jls10.pdf
[pike-talk]: https://www.youtube.com/watch?v=5kj5ApnhPAE
[unexported-twitter]: https://twitter.com/_jubobs_/status/1027995728692604928
