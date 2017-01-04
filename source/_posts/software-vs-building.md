---
title: software-vs-building-houses
date: 2016-09-13

---

# Software Developers coding on glass laptops shouldn't throw bricks
Reading the comments on [https://news.ycombinator.com/item?id=12795357] gave me some thoughts on the state of the art of building software vs the state of the art of building houses. It's one of the most favored comparisons one can make because of all the interesting differences that become apparent when viewing the two side by side. To summarize, one of the comments on the article: "Houses have been built for thousands of years and are relatively well understood, while each software project is basically like building a house except it might have 6 walls instead of 4, and you might need a new kind of nail that is a spiral, and actually aliens are going to live in it but you'll only find that out 6 months into the project."

## The approximate
So what makes building software so much less efficient than building a house? There are plenty of arguments on the subject, but one element I don't hear mentioned enough is the impossibility of approximation. When building things using conventional engineering, one has the ability to simulate, approximate, etc... the system at any given time and be rewarded with an understanding of how the system will function in reality. Now this is no silver bullet: simulations can be wrong, factors can be left unaccounted for, small issues can compound and present a bigger problem than when glossed over in an approximation. However, the fact that approximations can be made at all is extremely useful when designing systems.

With software, something like (finite element methods)[https://en.wikipedia.org/wiki/Finite_element_method] isn't really feasible. We'd love to be able to write some simplified pseudocode, run it, and be confident that we know the results carry over to our enormously complex 100k LOC accounting app. We try to deal with this by creating reusable abstractions that can be viewed as a black box. This much is known by any software developer. If we were able to abstract everything perfectly, then taken to the extreme, we'd be able to replace these modules with simplified versions and get an approximation of the software system as a whole. This obviously is impossible. Every abstraction ends up leaky from some perspective, and every detail ends up mattering given some change in your base assumptions.

## The way forward
Things like property based testing, advanced type systems, domain modelling are all attempts at gaining certainty that the system behaves as intended. They fulfill similar roles to simulation and approximation as it pertains to engineering, but are uniquely suited to the issues of software. Is it possible to go further?

### Property based testing
Tools like QuickCheck have sprung up for every language that seems capable of supporting it. The promise of using Property based testing is too good to ignore, but it hasn't quite reached the mainstream yet. In essence, you describe properties for your code that should hold for inputs of a given structure. You express these rules, and ways to generate the data for inputs and QuickCheck can make it much easier to determine whether your code works or not. For example, you can test a function foo(bar: Int), and QuickCheck can generate random integers for you, it could test integers that present edge cases like 0, negative numbers, numbers near an overflow, etc... Using this tool properly would ideally allow you to generalize about a class of inputs based on the approximation yielded by the data tested against. Unfortunately, not all business logic is convenient to be expressed in this manner.

### Free monads

Though lacking experience in using the (free monad)[https://wiki.haskell.org/Free_structure] in real systems, it seems promising. If the advocates of using it to represent business logic, we'd be granted an algebraic DSL which is interpreted by composeable interpreters of your domain logic. Being able to test the DSL separately from the side-effecting interpreters would be nice, but would it achieve our goals of having a representational approximation of the systems behavior? I'm optimistic, but I must assume it will not serve as a panacea for our software development woes.

### Alloy
Alloy is a "language and tool for relational models". Alloy gives you a tool for expressing relationships between elements in your domain, and a language for expressing intransients about them as well. Their example tutorial on modelling a file system in Alloy is extremely good at giving some context [http://alloy.mit.edu/alloy/tutorials/online/index.html]. Alloy takes the representation you've expressed and then tries to generate counterexamples that violate your intransients.
Example:
1. A filesystem node can either be a directory, a link or a file (simplification)
2. A directory can contain one or more filesystem nodes

Intransients:
1. every filesystem node must have a parent
2. no filesystem node can have itself as its parent
3. ...

If alloy can find a way to generate a filesystem node with itself as a parent, you'd invalidate the model. As with any software tool, using it has tradeoffs. What if you incorrectly model the problem? What if you fail to translate your model to software accurately? What if some operating characteristics of the system invalidate the assumptions the system was built on (ex: allowing concurrent filesystem modifications could lead to...issues).


### Summary
I'd love to have some answers on the subject. Planning on keeping this post open for modification as I learn more about the subjects mentioned within.
