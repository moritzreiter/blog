---
title: "Gist of Java's Local Variable Type Inference Style Guidelines"
date: 2025-12-15T10:43:04+01:00
draft: false
---

There's a [style
guide](https://openjdk.org/projects/amber/guides/lvti-style-guide) on when and
when not to use Local Variable Type Inference, which was introduced in Java 10.
It's published on the OpenJDK website, so I guess it can be regarded as
somewhat "official".

Even though the article states that overuse of the `var` keyword should be
avoided, in my reading it actually more or less boils down to this: If the code
is well structured in terms of local variable usage, i. e. the scope of local
variables is minimized, it's most of the time okay or even preferable to use
`var` for variable initialization.

The basic guiding principle when deciding is that it should be easy to figure
out the type of a variable by just reading the code, without having to rely on
IDE features.

For initializations that use a constructor or a factory method, the type should
easily be determinable by the name of the constructor or factory:

```java
// This is redundant:
Grumbelax grumbelax = new Grumbelax();

// This is fine:
var grumbelax = new Grumbelax();
var grumbelax = GrumbelaxFactory.create();
```

In other cases it's possible to convey the type information by chossing an
expressive variable name:

```java
// Consider this:
List<Snorbacle> result = TorfindleService.calculate();

// Here, type information would be lost to a reader
// without IDE support:
var result = TorfindleService.calculate();

// Changing the variable name can convey the type information
// to the reader again:
var snorbacles = TorfindleService.calculate();
```

But, if for some reason, the variable name `result` in the example is
preferable, then it's better to use the more verbose first form with the
explicit `List<Snorbacle>` declaration.

