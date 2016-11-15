---
layout: post
title: "Why I am ambivalent about object oriented programming"
---

# Introduction

Object oriented programming (OOP) was introduced with Simula in the 1960s and
refined with Smalltalk in the 1970s. Eventually the OOP paradigm became
extremely widely used, and today almost all popular programming languages are
"object oriented languages" or at least deliberately provide support for an OOP
approach. I'm not completely thrilled about OOP, and in this post I'm going to
describe some of the reasons why and also talk about some of the alternatives.

# OOP undermines the namespace or module system

Modern languages almost all have namespace or module systems that ensure we
don't have to worry too much about name collisions. And then OOP comes along and
completely subverts namespaces by requiring that all methods for a class belong
to one common namespace.

Imagine you've developed a new fast `Matrix` class.  You want it to support, on
the one hand, a `NumericArray` interface, which has a `multiply` method for
elementwise multiplication. But you also want it to support a `GenericMatrix`
interface, which has a `multiply` method for matrix multiplication.

Chances are this is a painful situation in your language. You probably simply
*can't* implement a class with both methods and will have to write some kind of
wrapper class to handle one of the interfaces. Actually, there's a sentiment in
the OOP world that this is a nonissue, because if your class needs to implement
two methods with the same name and signature, then your class is surely "doing
too many things" (see e.g., the comments
to
[this](http://stackoverflow.com/questions/2598009/method-name-collision-in-interface-implementation-java) Stack
Overflow question). To my mind, this is silly. I don't see why a name collision
in interfaces you're implementing is any less likely than a name collision
anywhere else.

What's the solution? The solution is not to give methods a special syntax
different from regular old functions. This is how it's done in the Common Lisp
Object System (available since the 1980s, with predecessors in the 1970s) and in
Haskell's type classes. For instance, in Haskell, if the `NumericArray`
interface (actually in Haskell the equivalent of interfaces are called
*classes*) lies in the `NA` module and the `GenericMatrix` interface lies in the
`GM` module, you can easily implement both:

```
instance NA.NumericArray Matrix where
	multiply x y = ...

instance GM.GenericMatrix Matrix where
	multiply x y = ...
```

(Note than in Haskell declaring a type to be an *instance* of a *class* is the
equivalent of letting it implement an interface in Java.)

You can later use one or the other function via `NA.multiply x y` or
`GM.multiply x y`.

# You can only implement extra methods or interfaces within the class definition

Now suppose your situation is somewhat different from what's described above.
Suppose there are already several matrix classes in common use. You're
developing a new mathematics library and have several functions which take
matrices as arguments. You want your users to be able to use either `FastMatrix`
or `SparseMatrix` or any of several other matrix classes in common
use. Moreover, you want people to be able to be able to use any future matrix
types they may implement. The obvious solution is to write a `GenericMatrix`
interface, and let `FastMatrix`, `SparseMatrix`, and anyone else implement
it. The problem is you don't have control over the `FastMatrix` or
`SparseMatrix` code and, even if you did, changing their code would be backwards
anyway: you don't want `FastMatrix` and `SparseMatrix` to depend on your
library.

This is another situation where in mainstream OOP languages you're pretty much
out of luck. You're going to have to write a wrapper class or come up with some
other workaround.

But, again, in Haskell, this is a nonissue because instance declarations (i.e.,
interface implementations) don't have to happen at the site where the type is
defined. We can just do
```
instance GenericMatrix FastMatrix where ...

instance GenericMatrix SparseMatrix where ...
```
when we define `GenericMatrix`.

By the way, this problem (the inability to add new functions to old data types)
and a related problem (the inability to add new subclasses to a type) are
together called
the [expression problem](https://en.wikipedia.org/wiki/Expression_problem).
This problem (and various solutions) have been known for a long, long time (and
largely ignored by the people creating mainstream programming languages, for
reasons I don't understand).

# OOP forces you into a limited paradigm

Bla
